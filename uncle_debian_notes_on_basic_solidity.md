
<img width="900" height="248"  alt="Untitled" src="https://github.com/debianchef/uncle-debian-notes/assets/108822895/237db375-50c9-4ca7-a4cd-958a3787afca">



## Table of Contents

## Getting started 
1. [Variables](#Variables)
2. [Ethereum Units (Wei, Gwei, Ether)](#ethereum-units-wei-gwei-ether)

## Concepts
3. [Arithmetic Operations](#arithmetic-operations)
4. [Conditional Statements (If)](#conditional-statements-if)
5. [Loops (For)](#loops-for)

## Types of Functions
6. [Public, External, Internal, Private, Pure and View](#functions)
7. [Constructor](#constructor-functions)
8. [Payable Functions](#payable-functions)
9. [Receive Function](#receive-function)
10. [Modifiers](#modifiers)
11. [Fallback Function](#fallback-function)

## Features
12. [Block Data (timestamp, number)](#block-data-timestamp-number)
13. [Events](#events)
14. [Inheritance](#inheritance)
15. [Interfaces](#interfaces)
16. [Understanding Evm, Storage, Opcodes](#evm)

## Token and Contract Interaction
17. [ERC20 Tokens](#erc20-tokens)
18. [ABI Encoding](#abi-encoding)
19. [msg.sender and address(this)](#msgsender-and-addressthis)

## Pattern
20. [Checks-effect-interaction pattern](#Checks-effect-interaction)



#### Variables
Solidity supports a variety of data types including:

1. `Address`

An address is a value  type that stores the location of an account on the Ethereum blockchain
```solidity
address myAddress = 0x5B38Da6a701c568545dCfcB03FcB875f56beddC4;
```

`Exercise`:
[Try in Remix](#remixLink)

2. `Bytes , Byte`

Bytes are reference types used to store fixed-size binary data. They store the location of the data in memory.

Example:

```solidity
bytes2 myBytes2 = 0x1234;
bytes32 myBytes32 = 0x1234567890abcdef1234567890abcdef12345678901234567890abcdef12345678;
```

`Exercise`:
[Try in Remix](#remixLink)

3. `String`

A string is a reference type that stores the location of a sequence of characters in memory.
```solidity
string myString = "Hello, World!";
```

`Exercise`:
[Try in Remix](#remixLink)

4. `Arrays`

Arrays are reference types that store references to a list of elements' memory locations.

```solidity
uint[] myArray = [1, 2, 3, 4, 5];
uint[5] myFixedArray = [1, 2, 3, 4, 5];
```

`Exercise`:
[Try in Remix](#remixLink)

5. `Structs`

A struct  is a `reference` variable because it stores the memory address of another variable, allowing indirect access to the value of that variable. Instead of holding the actual data, it points to the location in memory where the data is stored.

```solidity
struct User {
string name;
uint256 balance;
} 

//usage 
User john = User("John Doe", 30);
```
`Exercise`:
[Try in Remix](#remixLink)

6. `Enumerations`

Enumerations (enums) are user-defined types that consist of a set of named constants called elements or members. They store the location of these constants in `memory`

```solidity
enum Color {Red,
	Green,
	Blue

}

//usage 
Color myColor = Color.Green;
```

`Exercise`:
[Try in Remix](#remixLink)

>[!Note]
>Enums are internally represented as uint (unsigned integer). The first value in the enum has the value 0, the second value has the value 1, and so on.
>
>```console
>// Default value is always first element listed in
>// Returns uint
>//      Red, => 0
>//      Green, => 1
>//      Blue => 2
>```


7. `Integer`

Integers are value types that directly store the value within the variable itself.

```console
signed integers
Int8 —>   [-128 : 127]
Int16 —> [-32768 : 32767]
Int32 —> [-2147483648 : 2147483647]

unsigned integers
UInt8 — [0 : 255]
UInt16 — [0 : 65535]
UInt32 — [0 : 4294967295]
UInt64 — [0 : 18446744073709551615]
```

Examples

```solidity
int8 myInt8 = -127;
uint256 myUint256 = 12345678901234567890;
```
`Exercise`:
[Try in Remix](#remixLink)

>[!NOTE]
>Solidity reserves `256 bits` of storage regardless of the uint size


8. `Boolean`

A boolean is a value type that directly stores the true or false value within the variable `itself`.

```solidity
bool myBool = true; 
```

`Exercise`:
[Try in Remix](#remixLink)

>[!NOTE]
>A `reference` is a variable that stores the memory address of another variable, allowing indirect access to the value of that variable. Instead of holding the actual data, it points to the location in `memory` where the data is stored. Every reference type contains information on where it is `stored`


In Solidity, variables can be classified according to their data location. The data location specifies where the variable's value is stored.The  data locations include :

1. `Storage`: Variables with this data location are stored permanently on the blockchain
`

2. `Memory`: Variables with this data location are stored temporarily in memory and are erased after the function call completes.

3. `calldata`: Primarily used for external functions.. It behaves like a read-only version of memory, meaning you can't modify its contents.




#### Ethereum Units (Wei, Gwei, Ether)

Wei and Gwei are smaller units of Ether, used for more precise transactions.

```console
1 Ether (ETH) = 10^18 Wei
1 Ether (ETH) = 10^9 Gwei (Giga-Wei)
```



#### Arithmetic Operations

Just as other programing Languages , we can perform arithmetic operations exactly the same manner 

```console
int a = -10;
uint b = 5;
uint c = 3;
int sum = a + int(b); // Adding int and uint
uint exponentiation = b ** c; // Exponentiation of two uints
uint modulus = b % c; // Modulus of two uints
int difference = a - int(b); // Subtracting int and uint
int product = a * int(b); // Multiplying int and uint
int quotient = a / int(b); // Dividing int and uint
```
`Exercise`:
[Try in Remix](#remixLink)

>[!NOTE]
>In Solidity,  floats are not allowed. This is because they can lead to unexpected behaviours. For example dividing `5 by 3` might yield `1.6666` on one machine and `1.66667` on another. Such discrepancies can cause the blockchain network to disagree on transaction outcomes, leading to potential network splits. Therefore, Solidity avoids floats to ensure determinism and consensus. 



#### Conditional Statements (If)

If statements allow you to execute code based on conditions. The structure is similar to other programming languages. Here's a simple example:


```solidity
// SPDX-License-Identifier: MIT
pragma solidity ^0.8.0;

contract SimpleIfStatements {
    uint a = 10;
    uint b = 5;

    function checkValues() public view returns (string memory) {
		// If 'a' is greater than 'b'
        if (a > b) {
            return "a is greater than b";
        } else if (a == b) {
            return "a is equal to b";
        } else {
            return "a is less than b";
        }
    }
}

```
`Exercise`:
[Try in Remix](#remixLink)


>[!NOTE]
>`pragma solidity ^0.8.0;` is a directive that specifies the version of the Solidity compiler to use. It ensures that the contract is compiled with a version of Solidity that is compatible with 0.8.0 or any newer version that does not introduce breaking changes. This helps prevent issues that might arise from using an incompatible compiler version.

#### Loops

Solidity supports all the necessary loops just in other programming language.
`While` 
`do while` 
`for` 



`Exercise`:
[Try in Remix](#remixLink)


#### Public , External , Internal , Private Pure and View
In Solidity, a `function` is defined using the function keyword followed by the function name, parameters (if any), visibility specifier, and the function body.

```solidity

function functionName(parameters) visibility returns (returnType) {//function body}

//          |           |             |                   |             |
//          |           |             |                   |             |
//          ↓           ↓             ↓                   ↓             ↓
function Myfunction(uint anyname)    public  returns   (uint)    { return anyname;}
```

 Here's an example of defining functions with different visibility keywords in Solidity:

```solidity
pragma solidity ^0.8.0;

contract VisibilityExamples {
    uint256 public data;

  
    // Public function: Can be called internally, externally, and by derived contracts
    function setDataPublic(uint256 newData) public {
        data = newData;
    }

    // External function: Can only be called externally
    function setDataExternal(uint256 newData) external {
        data = newData;
    }

    // Internal function: Can be called internally and by derived contracts
    function _setDataInternal(uint256 newData) internal {
        data = newData;
    }

    // Private function: Can only be called within this contract
    function _setDataPrivate(uint256 newData) private {
        data = newData;
    }

    // Pure function: Does not read or modify state
    function pureFunction(uint256 a, uint256 b) public pure returns (uint256) {
        return a + b;
    }

    // View function: Reads state but does not modify it
    function viewFunction() public view returns (uint256) {
        return data;
    }
}

// A new contract that inherits the functionality of VisibilityExamples
contract ShowVisibilityExamples is VisibilityExamples {

    function callPublicFunction(uint256 newData) public {
        setDataPublic(newData); // Allowed: public function
    }


    function callInternalFunction(uint256 newData) public {
        _setDataInternal(newData); // Allowed: internal function
    }



     function callPrivateFunction(uint256 newData) public {
        _setDataPrivate(newData); // Not allowed: private function
     }
}

```



`Exercise`:
[Try in Remix](#remixLink)


>[!NOTE]
>The `is` keyword is used to denote inheritance. For example, `contract DerivedContract is ShowVisibilityExamples` means that `ShowVisibilityExamples` contract  inherits all the properties and functions of the `VisibilityExamples` contract. This allows `ShowVisibilityExamples` contract to use and extend the functionality defined in VisibilityExamples, promoting code reuse and organization

#### Constructor

A constructor is a special function in a smart contract that runs once when the contract is deployed. It initializes the contract's state and sets up variables or settings needed from the start. 

```solidity
pragma solidity ^0.8.0;

contract SimpleStorage {
    uint256 public data;

    // Constructor to initialize the data
    constructor(uint256 initialData) {
        data = initialData;
    }
}

// when the SimpleStorage contract is deployed, the constructor sets the initial value of data
```

`Exercise`:
[Try in Remix](#remixLink)


>[!NOTE]
> A constructor does not need the  `function` keyword to be declared just as in the example above. `Modifier`, `Receive`, `Fallback` are  also special functions that is  declared without `function` keyword.  

#### Modifiers
Consider `modifiers` as `Law enforcer` functions which helps ensure `certain conditions` are `met` before executing a function and  improving contract security.Modifiers are declared with the keyword `modifier` followed by the `name`

```solidity
pragma solidity ^0.8.0;

contract ModifiersExample {
    address public owner;

    // Modifier to check if the caller is the owner
    modifier onlyOwner() {
        require(msg.sender == owner, "Not the contract owner");
        _; 
    }

    // Constructor to set the contract owner
    constructor() {
        owner = msg.sender;
    }

    // Function that uses the onlyOwner modifier
    function changeOwner(address newOwner) public onlyOwner {
        owner = newOwner;
    }
}

```
modifier `onlyOwner()` checks if the caller is the owner and then executes the function code `_;`

>[!NOTE]
`msg.sender` is a global variable in Solidity that represents the `address` of the `account` that `called` or `initiated` the current `function`. It is used to `identify` who is `interacting` with the `contract`.You noticed that at  `onlyOwner()` modifier body ends with `_;` . This simply means if the conditions are met ,execute the function.

#### Payable Functions
Functions that can receive Ether are denoted by the payable keyword `payable`.

Example : 

```solidity
   function receiveEther() public payable {
        // Function body can remain empty
    }
```

[Try in Remix](#remixLink)

 When calling `receiveEther()`, you can send Ether along with the call



#### Receive Function
 This special function that can be implemented in a contract to handle plain Ether transfers sent to the contract without any data. The receive function is defined using the `receive` keyword and must be marked `payable`

 ```solidity
 receive() external payable {
    // Function body
}
  ```

[Try in Remix](#remixLink)


#### Fallback Function

When a function call is made to a contract, the data part of the call specifies which function to execute. If the call data does not match any function signature in the contract, the fallback function is triggered if it is defined

```solidity
pragma solidity ^0.8.0;

contract FallbackExample {
    address public owner;

    // Constructor to set the contract owner
    constructor() {
        owner = msg.sender;
    }

    // A function with a specific signature
    function setOwner(address newOwner) public {
        owner = newOwner;
    }

    // Fallback function to handle unmatched calls
    fallback() external payable {
        // Handle unmatched calls or Ether transfers
    }
}
```

The `setOwner()` function expects a parameter of type `address`. If a call is made with `data` that doesn't `match` this expected `signature`, the `fallback` function will be `triggered` if it is `defined` in the contract

[Try in Remix](#remixLink)


## Block Data (timestamp, number)
Solidity provides access to certain properties of the blockchain, such as block data.
Two commonly used block properties are: 

1. `block.timestamp`: This provides the `timestamp` of the current block, which is the approximate time when the block was mined. It is often used for time-based conditions in smart contracts
Example: 
```solidity
    // Function to get the current block timestamp
    function getCurrentTimestamp() public view returns (uint256) {
        return block.timestamp;
    }
```


2. `block.number`: This provides the `number` of the `current block`. It can be used to measure time in `terms` of `block`s rather than `seconds`.

```solidity
    // Function to get the current block number
    function getCurrentBlockNumber() public view returns (uint256) {
        return block.number;
    }
```


 ## Events

When an `event` is emitted, it creates a log that can be accessed on the blockchain.

```solidity
pragma solidity ^0.8.0;

contract EventExample {

	  uint256 public data;

// You can declare as many type  and parameter as you want to emit logs 
    event EventName(  type1       parameter1      type2    parameter2   )

//          |           |             |            |         |
//          |           |             |            |         |
//          ↓           ↓             ↓            ↓         ↓
    event DataChanged(address indexed user,     uint256 newValue);


// Index Keyword is declared to filter logs
  

    // Function to change the data and emit an event
    function changeData(uint256 newData) public {
        uint256 oldData = data;
        data = newData;

		// Call the event and pass the expected parameter to emit logs 
        emit DataChanged(msg.sender,oldData, newData); // Emit the event
    }
}

```

[Try in Remix](#remixLink)

>[!NOTE]
> Events are a crucial feature in Solidity for logging actions and  they help in track state changes. 



## Inheritance
 By now we should be familiar with the keyowrd `is` which is declared  to allows a contract to inherit properties and functions from another contract.


 ```solidity
pragma solidity ^0.8.0;

contract BaseContract {
    uint256 public data;

   
// A function to get data
    function getData() public view virtual returns (uint256) {
        return data;
    }
}


// Inherit all properties from BaseContract contract 
contract DerivedContract is BaseContract {
   
 function getDataFromBaseContract() public view returns (uint256) {
    // Call getData function
	    return super.getData() 
		}

}

 ```


In case we need to use functionalities of another contract without inheriting its properties , we can use `Composition`.

How It Works
1. Instance Creation: A contract creates an instance of another contract.
2. Function Calls: The contract interacts with the instance by calling its functions.

```solidity
pragma solidity ^0.8.0;

contract BaseContract {
    uint256 public data;

    // A function to set data
    function setData(uint256 newData) public {
        data = newData;
    }

    // A function to get data
    function getData() public view virtual returns (uint256) {
        return data;
    }
}

```

```solidity
pragma solidity ^0.8.0;

import "./BaseContract.sol"; // Import the BaseContract

contract UsingComposition {
    BaseContract baseContract;

    // Constructor to initialize the instance of BaseContract
    constructor(address baseContractAddress) {
        baseContract = BaseContract(baseContractAddress); // Initialize the instance with the deployed contract address
    }

    // Function to get data from the BaseContract
    function getDataFromBaseContract() public view returns (uint256) {
        return baseContract.getData(); // Call getData function from BaseContract
    }

    // Function to set data in the BaseContract
    function setDataInBaseContract(uint256 newData) public {
        baseContract.setData(newData); // Call setData function from BaseContract
    }
}

```

In this example above , we will create a contract `UsingComposition` that creates an instance of `BaseContract` and interacts with it.
 
 [Try in Remix](#remixLink)


## Interfaces

Interfaces in Solidity are used to define the functions that a contract must implement without providing the actual implementation.

Key Features
1. `Function Signature`s: Only function signatures are defined, without any implementation.
2. `No State Variables`: Interfaces cannot have state variables.
3. `No Constructors`: Interfaces cannot have constructors.
4. `No Function Modifiers`: Functions cannot have modifiers like public, internal, etc.

```solidity
pragma solidity ^0.8.0;

interface IExample {
    function setDate(uint256 _value) external;
    function getData() external view returns (uint256);
}

```
Implementation

```solidity
pragma solidity ^0.8.0;

import "./IExample.sol";

contract Example is IExample {
    uint256 private value;

    // Implement the setValue function
    function setData(uint256 _value) external override {
        value = _value;
    }

    // Implement the getValue function
    function getData() external view override returns (uint256) {
        return value;
    }
}

```
[Try in Remix](#remixLink)

>[!NOTE]
> By using interfaces, you can ensure that your contracts adhere to specific standards, making them easier to interact with and maintain.


## Understanding Evm, Storage, Opcodes
#### Evm
Imagine you have a magic robot (ethereum virtual Machine in short EVM) that can follow special instructions (smart contracts) to do tasks. This robot always does the tasks in the same way, so everyone watching the robot agrees on what it did, no matter where they are


`Key Features of Evm` 
1. Turing-complete: Can execute any computation given enough resources.
2. Deterministic: Ensures the same inputs produce the same outputs.
3. Isolated: Each contract runs in isolation, preventing interference between contracts.

Just like programs written in other programming languages, smart contracts  are compiled into bytecode. Bytecode is a low-level, machine-readable representation of the contract that the Ethereum Virtual Machine (EVM) can execute. Since evm  does not directly understand solidity or any other language used to write a contract , it needs to be translated/converted into bytecode by the  compilier.  


#### Storage
Think of storage like a big toy box where you keep your toys (data). Putting a toy in the box (writing data) is a bit hard and takes time (costs more gas), but once it’s in the box, it stays there safely. If you just want to look at your toy (read data), it’s easier and quicker.


Key Concepts
1. Storage Slots: Each state variable is stored in a specific slot.[readmore](#storage)
2. Gas Costs: Writing to storage is expensive, so optimizing storage usage is crucial.[readmore](#storage)
3. Mappings and Arrays: Common data structures that interact with storage.


>[!IMPORTANT]
>`Gas` is a unit of measurement that represents the amount of computational effort required to execute operations on the Ethereum network. Every operation performed by the Ethereum Virtual Machine (EVM) has an associated gas cost. By requiring gas for transactions, Ethereum mitigates the risk of Denial-of-Service (DoS) attacks.

#### Opcodes
`Opcodes` are like the instructions you give to the magic robot (EVM) to do things. Each instruction is very simple, like "add two numbers" or "put a toy in the box." By giving the robot a series of these simple instructions, you can make it do very clever and complex tasks. `Opcodes` are `low-level` instructions executed by the EVM. Each operation (e.g., arithmetic, data access) has a specific opcode. Understanding opcodes helps in writing gas-efficient contracts 

Key Opcodes
```console
ADD: Addition operation
MUL: Multiplication operation
SLOAD: Load from storage
SSTORE: Store to storage
CALL: Calls another contract
```


[More Opcodes](#opcodes)
 
In practice, you rarely write opcodes directly, but tools like assembly language in Solidity (inline assembly) allow for optimized operations


Example of Using Opcodes
```solidity
pragma solidity ^0.8.0;

contract OpcodeExample {

    function add(uint256 a, uint256 b) public pure returns (uint256 result) {
        
		// inline assembly
		assembly {
            result := add(a, b) // Directly using the ADD opcode
        }
    }
}

```
[Try in Remix](#remixLink)

## ERC20 Tokens
ERC20 tokens are a standardized way of creating and managing tokens on the Ethereum blockchain. They provide interoperability, fungibility, and transferability, making them widely used in various decentralized applications and platforms.

Core ERC20 Functions
ERC20 tokens must implement the following functions:



```solidity
// Total Supply: Returns the total supply of tokens.
function totalSupply() public view returns (uint256);



//Balance Of: Returns the token balance of a specific address.
function balanceOf(address account) public view returns (uint256);



// Transfer: Transfers a certain amount of tokens to a specific address.
function transfer(address recipient, uint256 amount) public returns (bool);



//Allowance: Returns the remaining number of tokens that a spender is allowed to spend on behalf of the owner.
function allowance(address owner, address spender) public view returns (uint256);



//Approve: Allows a spender to spend a certain amount of the owner’s tokens.

function approve(address spender, uint256 amount) public returns (bool);


//Transfer From: Transfers tokens from one address to another using the allowance mechanism.
function transferFrom(address sender, address recipient, uint256 amount) public returns (bool);
```


ERC20 Events

ERC20 tokens must emit the following events:



```solidity
//Transfer: Emitted when  you  transfer a certain amount of tokens to a specific address.
event Transfer(address indexed from, address indexed to, uint256 value);


//Approval: Emitted when the allowance of a spender for an owner is set by a call to approve.
event Approval(address indexed owner, address indexed spender, uint256 value);
```

In the OpenZeppelin [GitHub repository](#https://github.com/OpenZeppelin/openzeppelin-contracts/blob/master/contracts/token/ERC20/ERC20.sol)  you can find the standard ERC20 token implementation and other useful contracts

[Try in Remix](#remixLink)


## ABI Encoding
ABI (Application Binary Interface) encoding is a way to encode and decode data when interacting with smart contracts on the Ethereum blockchain.


Just like fingerprints uniquely identify people, every function in a smart contract has a unique signature that identifies it on the Ethereum network. When you "call" a smart contract, you're sending a message on the Ethereum network with specific information. This information includes the function's unique signature and any necessary data, so the smart contract knows exactly which function to execute.

There are many data encodings, json, xml, etc. Solidity and ethereum use the ABI encoding.

Key Components
1. Function Selector: The first 4 bytes of the encoded data, derived from the function signature .
2. Arguments: The parameters passed to the function, encoded according to their types.


Consider the following Solidity function:

```solidity
function transfer(address recipient, uint256 amount) public returns (bool);
```

To call this function with recipient 0x123... and amount 1000, we encode the data as follows:


```console
1. Function Selector: a9059cbb // name of the funtion

2. Arguments: Encoded using ABI encoding rules:
Address: 0000000000000000000000001234567890123456789012345678901234567890
Uint256: 00000000000000000000000000000000000000000000000000000000000003e8 (1000 in hex)
```

Final encoded data:

```console
a9059cbb
0000000000000000000000001234567890123456789012345678901234567890
00000000000000000000000000000000000000000000000000000000000003e8
```

Solidity provides built-in functions for ABI encoding:

```solidity
// abi.encode: Encodes data without adding the function selector.
abi.encode(uint256(100), address(0x1234567890123456789012345678901234567890))



// abi.encodePacked: Similar to abi.encode, but produces a more compact encoding.
abi.encodePacked(uint256(100), address(0x1234567890123456789012345678901234567890))


// abi.encodeWithSelector: Encodes data with a given function selector.
abi.encodeWithSelector(0xa9059cbb, address(0x1234567890123456789012345678901234567890), uint256(1000))


// abi.encodeWithSignature: Encodes data with a function signature.
abi.encodeWithSignature("transfer(address,uint256)", address(0x1234567890123456789012345678901234567890))
```

Example

```solidity
pragma solidity ^0.8.0;

contract ABIExample {

    function encodeTransfer(address recipient, uint256 amount) public pure returns (bytes memory) {
        return abi.encodeWithSignature("transfer(address,uint256)", recipient, amount);
    }
}
```

[Try in Remix](#remixLink)

## Msg.sender and Address(this)

This is very straight forward By now you have seen  msg.sender but lets dive a bit deeper to understand how and when its used in a smart contract 

`msg.sender` global variable has some key features 

`Caller Identification`: Determines who initiated the function call.
`Access Control`: Often used to restrict functions to specific users.
`Payments`: Can track who sent Ether to the contract.


```solidity
pragma solidity ^0.8.0;

contract Example {
    address public owner;

    constructor() {
        owner = msg.sender; // Set the deployer as the owner
    }

    function setOwner(address newOwner) public {
        require(msg.sender == owner, "Only the owner can set a new owner");
        owner = newOwner;
    }
}

```

In this example:

1. The `constructor()` sets the contract deployer as the owner.
2. The `setOwner()` function allows only the current owner to change the ownership.


`address(this)` is a keyword in that represents the address of the current contract. It is used to refer to the contract itself, allowing interactions with its own address and balance.

Key Points:
1. Contract Address: Represents the contract’s own address.
2. Self-Interactions: Enables the contract to call its own functions or interact with its own balance.
3. Ether Balance: Can be used to check the contract's Ether balance.

Examples:

```solidity
pragma solidity ^0.8.0;

contract Example {
    // Function to get the contract's address
    function getContractAddress() public view returns (address) {
        return address(this);
    }

    // Function to get the contract's Ether balance
    function getContractBalance() public view returns (uint256) {
        return address(this).balance;
    }


}

```


## Checks-effect-Interaction pattern
When it comes to writing smart contracts there is a secure pattern to follow. The `Checks-Effects-Interactions` pattern is a best practice in Solidity development that helps prevent reentrancy attacks and ensures safe smart contract interactions. This pattern involves three steps executed in a specific order:

1. Checks: Validate all conditions and inputs at the beginning of the function.
2. Effects: Update the contract’s state variables.
3. Interactions: Interact with external contracts and transfer funds.

#### Why Use This Pattern?

1. Prevent [Reentrancy](#reentrancy) Attacks: By updating the contract’s state before making external calls, it mitigates the risk of reentrancy attacks, where an attacker could exploit the external call to repeatedly re-enter the function and manipulate state.

2. Ensure Safety: It ensures that the contract’s state is updated correctly before any external interactions, reducing the risk of unexpected behaviors or bugs.


#### 1. Negative Example (Not Using Checks-Effects-Interactions)
```solidity 

    // Unsafe withdrawal function without using Checks-Effects-Interactions pattern
    function withdraw(uint256 amount) public {
        // Interactions
        (bool success, ) = msg.sender.call{value: amount}("");
        require(success, "Transfer failed");

        // Checks
        require(balances[msg.sender] >= amount, "Insufficient balance");

        // Effects
        balances[msg.sender] -= amount;
    }

 

```
Explanation:

`Interactions`: Transfers Ether to the user before updating the state.
`Checks`: Verifies the user has enough balance after the transfer.
`Effects`: Updates the user's balance after the external interaction.


This pattern is vulnerable to [reentrancy](#reentrancy) attacks because the state is not updated before making an external call. An attacker could exploit this by repeatedly calling the withdraw function before the balance is updated, draining the contract.


#### 2. Positive Example (Using Checks-Effects-Interactions)

```solidity

    // Safe withdrawal function using Checks-Effects-Interactions pattern
    function withdraw(uint256 amount) public {
        // Checks
        require(balances[msg.sender] >= amount, "Insufficient balance");

        // Effects
        balances[msg.sender] -= amount;

        // Interactions
        (bool success, ) = msg.sender.call{value: amount}("");
        require(success, "Transfer failed");
    }


```

Explanation:

`Checks`: Ensures the user has enough balance to withdraw.
`Effects`: Updates the user's balance before interacting with external contracts.
`Interactions`: Transfers Ether to the user after updating the state.


>[!IMPORTANT]
>This pattern helps prevent reentrancy attacks by ensuring the state is correctly updated before any external interaction


By adhering to the Checks-Effects-Interactions pattern, you can write more secure and robust smart contracts

## Developing and Deploying Contracts



The link below introdues you foundry.  Learn how to write , test and deploy smart contracts locally . Yessss locally using your favourite IDE prefferably vs-code and [foundry]((https://book.getfoundry.sh/)). There is no special reason for choosing vs-code. 
What matters the most is practicing what youve learnt. In the next episode , i will include project ideas to try your hands on . 

You can install Foundry using the following command:

```bash
curl -L https://foundry.paradigm.xyz | bash
```

Initialize a new project:

```bash

forge init MyProject
```

We can also integrate foundry into an existing smart contract project. 

[Foundry Tutorials](https://github.com/debianchef/uncle-debian-notes/blob/trunk/uncle_debian_notes_on_foundry.md)



![8t8d9w](https://github.com/debianchef/uncle-debian-notes/assets/108822895/4ab6ffa8-ab34-4a16-9f09-828968a2ef9e)


Congratulations!!!. You've just mastered some key concepts of Ethereum and Solidity.
