# Solidity Basics

## Table of Contents

## Getting started 
1. [Variables](#Variables)
2. [Ethereum Units (Wei, Gwei, Ether)](#ethereum-units-wei-gwei-ether)

## Concepts
3. [Arithmetic Operations](#arithmetic-operations)
4. [Conditional Statements (If)](#conditional-statements-if)
5. [Loops (For)](#loops-for)
6. [Structs](#structs)


## Types of Functions
7. [Constructor Functions](#constructor-functions)
8. [Require Statement](#require-statement)
9. [Payable Functions](#payable-functions)
10. [Receive Function](#receive-function)
11. [Modifiers](#modifiers)

## Token and Contract Interaction
12. [ERC20 Tokens](#erc20-tokens)
13. [ABI Encoding](#abi-encoding)
14. [Interacting with Other Contracts](#interacting-with-other-contracts)
15. [msg.sender and address(this)](#msgsender-and-addressthis)

##  Features
16. [Block Data (timestamp, number)](#block-data-timestamp-number)
17. [Events](#events)
18. [Inheritance](#inheritance)
19. [Interfaces](#interfaces)
20. [Evm, Storage, Opcodes](#evm)

## Pattern
21.  [Checks-effect-interaction pattern](#Checks-effect-interaction)


#### Variables
Solidity supports a variety of data types including:

1. Address

An address is a value  type that stores the location of an account on the Ethereum blockchain
```solidity
address myAddress = 0x5B38Da6a701c568545dCfcB03FcB875f56beddC4;
```

2. Bytes

Bytes are reference types used to store fixed-size binary data. They store the location of the data in memory.
```solidity
bytes2 myBytes2 = 0x1234;
bytes32 myBytes32 = 0x1234567890abcdef1234567890abcdef12345678901234567890abcdef12345678;
```
3. String

A string is a reference type that stores the location of a sequence of characters in memory.
```solidity
string myString = "Hello, World!";
```

4. Arrays

Arrays are reference types that store references to a list of elements' memory locations.

```solidity
uint[] myArray = [1, 2, 3, 4, 5];
uint[5] myFixedArray = [1, 2, 3, 4, 5];
```

5. Structs

A struct  is a `reference` variable because it stores the memory address of another variable, allowing indirect access to the value of that variable. Instead of holding the actual data, it points to the location in memory where the data is stored.

```solidity
struct User {
    string name;
    uint256 balance;
} 

//usage 
User john = User("John Doe", 30);
```

6. Enumerations
Enumerations (enums) are user-defined types that consist of a set of named constants called elements or members. They store the location of these constants in memory

```solidity
enum Color {Red, Green, Blue}

//usage 
Color myColor = Color.Green;
```

7. Integer

Integers are value types that directly store the value within the variable itself.
signed integers
Int8 —>   [-128 : 127]
Int16 —> [-32768 : 32767]
Int32 —> [-2147483648 : 2147483647]

unsigned integers
UInt8 — [0 : 255]
UInt16 — [0 : 65535]
UInt32 — [0 : 4294967295]
UInt64 — [0 : 18446744073709551615]


solidity
```solidity
int8 myInt8 = -127;
uint256 myUint256 = 12345678901234567890;
```
>[!NOTE]
>Solidity reserves 256 bits of storage regardless of the uint size


8. Boolean

A boolean is a value type that directly stores the true or false value within the variable itself.

```solidity
bool myBool = true;
```

>[!NOTE]
>A `reference` is a variable that stores the memory address of another variable, allowing indirect access to the value of that variable. Instead of holding the actual data, it points to the location in memory where the data is stored. Every reference type contains information on where it is stored


In Solidity, variables can be classified according to their data location. The data location specifies where the variable's value is stored.The  data locations include :

1. Storage: Variables with this data location are stored permanently on the blockchain
`

2. Memory: Variables with this data location are stored temporarily in memory and are erased after the function call completes.

3. calldata: Primarily used for external functions.. It behaves like a read-only version of memory, meaning you can't modify its contents.

#### Ethereum Units (Wei, Gwei, Ether)

Wei and Gwei are smaller units of Ether, used for more precise transactions.

1 Ether (ETH) = 10^18 Wei
1 Ether (ETH) = 10^9 Gwei (Giga-Wei)

#### Arithmetic Operations

#### Conditional Statements (If)







