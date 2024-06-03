## Development 

To get started, we will learn solidity as a language.
Let’s create a hello world using foundry.

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

>[!NOTE]
> If you’re on Windows, you will need to install and use Git BASH or WSL, as your terminal


This will install Foundryup, then simply follow the instructions on-screen, which will make the foundryup command available in your CLI

After installation , Lets run the  command below  in terminal  to creates a new directory `MyfirstContract`   using foundry default template and  also initialize a new git repository

```bash
forge init MyfirstContract --no-commit
```



Your Project Directory should look like this .

![alt text](image.png)


# Project Layout

We can see that some starter files has been downloaded in our workspace. Lets walkthrough : 

 1. The `/lib` folder is where all  downloaded libraries  will be stored. (dependencies are stored as git submodules)

 2. The  `/script` folder is where we will be writing our deploy script.

 3. The `/src` folder is where we will be writing our contract (default directory for contracts)

 4. The `/test` folder is where we will be writing test for all the contracts.(default directory for tests)

We can also see that there are files inside these folders with `.sol` extentions.  These files are solidity files
 




![alt text](image-1.png)


To compile the code we run the following command :

```bash
forge build  
```

![alt text](image-2.png)





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


function test_helloWorld () public {
   uint256 number = 100;
   uint256 result = helloWorldcontract.helloWorld();
assertEq(number , result);
}



}
```

Now  copy or type the code in the new file created in the `/test` folder and run the command

```bash
forge test --mt  test_helloWorld_function 
```


This command will look inside your test folder for a test function called `test_helloWorld_function`
Remember to add `test` before your function name since foundry uses that for function calls. In the case below 
we added `test` to `_helloWorld_function`  .


To display output add flag -vvvv :
```bash
forge test --mt  test_helloWorld_function -vvvv
```

To run all test incase we have multiple function calls :

```bash
forge test 
```


![alt text](image-3.png)

