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

After installation , run the following command to create , navigate to MyfirstContract directory and initialize the foundry project to develop our contract.

```bash
mkdir MyfirstContract && cd MyfirstContract && forge init --no-commit
```



Your Project Directory should look like this .

![alt text](image.png)


We can see that some starter files has been downloaded in our workspace. Lets walkthrough : 

 1. The `/lib` folder is where all  downloaded libraries or dependancies  will be placed. 

 2. The  `/script` folder is where we will be writing our deploy script.

 3. The `/src` folder is where we will be writing our contract (main project dir)

 4. The `/test` folder is where we will be writing test for all the contracts.

We can also see that there are files inside these folders with `.sol` extentions.  These files are solidity files
 


Now lets go ahead and create a new file `MyHelloWorld.sol` in the `/src` folder and paste our contract code . Note that the name does not matter. You can name it anything.

![alt text](image-1.png)


