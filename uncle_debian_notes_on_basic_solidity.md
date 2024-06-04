# Solidity Basics
---
## Table of Contents

## Getting Started with Solidity
1. [Variables](#Variables)
2. [Constants](#constants)
5. [Ethereum Units (Wei, Gwei, Ether)](#ethereum-units-wei-gwei-ether)

## Core Programming Concepts
6. [Arithmetic Operations](#arithmetic-operations)
7. [Conditional Statements (If)](#conditional-statements-if)
8. [Loops (For)](#loops-for)
9. [Structs](#structs)

## Working with Data
10. [Arrays and Strings](#arrays-and-strings)
11. [Mappings](#mappings)

## Functions and Execution
12. [Constructor Functions](#constructor-functions)
13. [Require Statement](#require-statement)
14. [Payable Functions](#payable-functions)
15. [Receive Function](#receive-function)

## Token and Contract Interaction
16. [ERC20 Tokens](#erc20-tokens)
17. [ABI Encoding](#abi-encoding)
18. [Interacting with Other Contracts](#interacting-with-other-contracts)
19. [msg.sender and address(this)](#msgsender-and-addressthis)

## Blockchain Specific Features
20. [Block Data (timestamp, number)](#block-data-timestamp-number)
21. [Events](#events)

## Advanced Solidity Features
22. [Inheritance](#inheritance)
23. [Interfaces](#interfaces)
24. [Modifiers](#modifiers)


#### Variables

Solidity supports a variety of data types including:

1. Address
2. Bytes
3. String
4. Arrays
5. Structs
6. Enumerations
7. Integer
8. Boolean



1. Address
```solidty
solidityCopy codeaddress myAddress = 0x5B38Da6a701c568545dCfcB03FcB875f56beddC4;
```

2. Bytes
```solidty
solidityCopy codebytes2 myBytes2 = 0x1234;
bytes32 myBytes32 = 0x1234567890abcdef1234567890abcdef12345678901234567890abcdef12345678;
```
3. String
```solidty
solidityCopy codestring myString = "Hello, World!";
```

4. Arrays
```solidty
solidityCopy codeuint[] myArray = [1, 2, 3, 4, 5];
uint[5] myFixedArray = [1, 2, 3, 4, 5];
```

5. Structs
```solidty
solidityCopy codestruct Person {
    string name;
    uint age;
}

Person john = Person("John Doe", 30);
```

6. Enumerations
```solidty
solidityCopy codeenum Color {Red, Green, Blue}

Color myColor = Color.Green;
```

7. Integer
```solidty
solidityCopy codeint8 myInt8 = -127;
uint256 myUint256 = 12345678901234567890;
```

8. Boolean
```solidty
solidityCopy codebool myBool = true;
```

#### Immutable Variables

#### Constants

####

####







