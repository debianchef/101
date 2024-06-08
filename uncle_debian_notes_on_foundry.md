 This article assumes the reader is familar with [Solidity Programing Language](https://github.com/debianchef/uncle-debian-notes/blob/trunk/uncle_debian_notes_on_basic_solidity.md) .


# Setup your Environment

To get started, 
Let’s create a hello world contract using foundry.

```solidity

contract MyHelloWorldContract {

	function helloWorld() public pure returns (uint256) {
		return 100;
	}
}
```

First we need to make sure  we have foundry installed .

Open your terminal and run the following command:
```bash
curl -L https://foundry.paradigm.xyz | bash
```
---
>[!NOTE]
> If you’re on Windows, you will need to install and use Git BASH or WSL, as your terminal
---

This will install Foundryup, then simply follow the instructions on-screen, which will make the foundryup command available in your CLI

After installation , Lets run the  command below  in terminal  to creates a new directory `MyfirstContract`   using foundry default template and  also initialize a new git repository

```bash
forge init MyfirstContract --no-commit
```
---
>[!NOTE]
>Foundry is a development framework to make testing, development, and deployment easier.Forge is a command-line tool that ships with Foundry. Forge  tests, builds, and deploys your smart contracts
---

Your Project Directory should look like this .


![image-5](https://github.com/debianchef/uncle-debian-notes/assets/108822895/4deaa8a0-64d6-41ab-a9d2-7696a15b957f)


#### Project Layout

We can see that some starter files has been downloaded in our workspace. Lets walkthrough : 

 1. The `/lib` folder is where all  downloaded libraries  will be stored. (dependencies are stored as git submodules)

 2. The  `/script` folder is where we will be writing our deploy script.

 3. The `/src` folder is where we will be writing our contract (default directory for contracts)

 4. The `/test` folder is where we will be writing test for all the contracts.(default directory for tests)

We can also see that there are files inside these folders with `.sol` extentions.  These files are solidity files
 


#### Imports 

We can run below command to see how forge is  mapping out  dependencies ;

```bash
forge re
```
or 

```bash
forge remappings
```

![image-4](https://github.com/debianchef/uncle-debian-notes/assets/108822895/7da65357-46d3-4af1-9dd3-065dce824700)


forge-std/ can be found(=) or (maps to ) in the lib/forge-std/src/ directory 

We can now craft our import statement as follows

```bash
import "forge-std/Test.sol"
```

We can also import our contract by crafting the import statement assuming we want to import our MyfirstContract contract  and call its functions

```bash
import {MyHelloWorldContract} from "../src/MyHelloWorld.sol";
```


To compile the code we run the following command :

```bash
forge build  
```

![image-6](https://github.com/debianchef/uncle-debian-notes/assets/108822895/ca5c8609-5dad-463b-a76b-923a5a5611a9)


# Testing


The test code should look something like this 

```solidity
// SPDX-License-Identifier: UNLICENSED
pragma solidity ^0.8.13;
import {Test} from "forge-std/Test.sol";
import {MyHelloWorldContract} from "../src/MyHelloWorld.sol";

contract MyHelloWorldTest is Test {
MyHelloWorldContract helloWorldcontract;

    function setUp() public {
        helloWorldcontract = new MyHelloWorldContract();
    }


function test_helloWorld_function () public {
   uint256 number = 100;
   uint256 result = helloWorldcontract.helloWorld();
assertEq(number , result);
}



}
```
---
>[!NOTE]
>You noitced that the test contract  ends with .t.sol
---

Now  copy or type the code in the `MyHelloWorld.t.sol` created in the `/test` folder and run the command :

To run all test incase we have multiple function :

```bash
forge test 
```

Since we only have a single function and we want to  run only that, we can use the command :

```bash
forge test --mt  test_helloWorld_function 
```
This  will  search inside your project  for a test function called `test_helloWorld_function`.

---
>[!IMPORTANT]
> Remember to add `test` before your function name. This is because in foundry, contract with a function that starts with test is considered to be a test.
--- 

In the our case  we added `test` to `_helloWorld_function`  .



To display output add flag -vvvv :
```bash
forge test --mt  test_helloWorld_function -vvvv
```

We can also run 
```bash 
forge test --match-contract MyHelloWorldTest --match-test test_helloWorld_function -vvvv
```
to specifically  call the `test_helloWorld_function` in the `MyHelloWorldTest` contract and display output.


The test should pass without any issues 


![image-3](https://github.com/debianchef/uncle-debian-notes/assets/108822895/e7a2bb14-f984-4eb7-83f6-d71a90656961)


We can see that there a new function  called `setUp()`.In foundry we use it to setup  the your imported contract for test functions to properly operate.We can also see that inside the the setUp() function there is a declaration .

>[!IMORTANT]
>Pay close attention to the spelling of the   function `setUp()` .

we use this line of code to deploy a fresh instance of `MyHelloWorldContract` before each test case is ran. 
```solidiy
helloWorldcontract = new MyHelloWorldContract();
```

#### Assertions

Function helloWorld() in  MyHelloWorldContract.sol returns `100` any time its called. To verify that the function will return 100 , we declared a local  
```solidity
  uint256 number = 100;
```
 `assertEq` is used to compare  two values will be equal. Example `a==b`. Read more on 
[assertions](https://book.getfoundry.sh/reference/forge-std/assertEq)  in foundry  




####  Cheatcodes


Lets add an input parameter to   function `HelloWord()`


![image-9](https://github.com/debianchef/uncle-debian-notes/assets/108822895/f9c2de97-9ea4-4bac-89e0-109859628a9f)


And the test function 



![image-10](https://github.com/debianchef/uncle-debian-notes/assets/108822895/4eec885a-380b-4c08-ad94-3eac92177acd)


 `vm.prank(Alice);` and `vm.assume(number > 99);`  are foundry [cheatCode](https://book.getfoundry.sh/cheatcodes/).You do serveral things with them.
 1. Change identity  `vm.prank(Alice);`
 2. inject specific conditions as true `vm.assume(number > 99);`.


 To execute a cheatcode function you will have to `import {Test} from "forge-std/Test.sol";`  and inherit all functions from the Test contract found in the `/lib/forge-std` directory

 

 # Traces

By now you have already seen that forge can produce traces for test by adding -vvvv or -vv

![image](https://github.com/debianchef/uncle-debian-notes/assets/108822895/9f02a7b4-b6c7-46b8-b91e-840b53c9b48f)


 Traces above  follows the general format below:

```solidity
  [<Gas Usage>] <Contract>::<Function>(<Parameters>)
    ├─ [<Gas Usage>] <Contract>::<Function>(<Parameters>)
    │   └─ ← <Return Value>
    └─ ← <Return Value>
```


Colors associated with traces has variety of meanings

Green: For calls that do not revert

Red: For reverting calls

Blue: For calls to cheat codes

Cyan: For emitted logs

Yellow: For contract deployments



# Deployment 




![8t8ceo](https://github.com/debianchef/uncle-debian-notes/assets/108822895/06bcdb50-3de0-4536-8ce0-4b394055a783)
