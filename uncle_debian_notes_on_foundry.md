## Development 

To get started, we will learn solidity as a language.
Let’s create a hello world using foundry.

First we need to make sure  we have foundry installed .

Open your terminal and run the following command:
```bash
curl -L https://foundry.paradigm.xyz | bash
```

>[!NOTE]
> If you’re on Windows, you will need to install and use Git BASH or WSL, as your terminal


This will install Foundryup, then simply follow the instructions on-screen, which will make the foundryup command available in your CLI

After installation , create a new directory where we will be creating our `MyHelloWorldContract`. 

```bash
mkdir MyfirstContract && cd MyfirstContract && forge init --no-commit
```

This one liner command will create , navigate to MyfirstContract directory and initialize the foundry project to develop our contract 

Your Project Directory should look like this .
![alt text](image.png)



```solidity

contract MyHelloWorldContract {

	function helloWorld() public pure returns (uint256) {
		return 100;
	}
}
```