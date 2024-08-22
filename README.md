## ERC20 Token Standard 

This repository contains a custom ERC20 token contract written in Solidity. The contract is based on OpenZeppelin's ERC20 implementation and includes additional functionalities for minting, burning, and custom transfers.

## Contract Overview

The `Custom_ERC20` contract is an extension of the standard ERC20 token. It allows the deployment of a token with a customizable name, symbol, and initial supply. The contract includes additional functions to mint and burn tokens, as well as a custom transfer function.

### Features

- **Minting**: The contract owner can mint additional tokens to any address.
- **Burning**: Token holders can burn (destroy) their tokens.
- **Custom Transfer**: A specialized transfer function with an added requirement to prevent transfers to the zero address.

## Contract Code

```solidity
// SPDX-License-Identifier: MIT
pragma solidity ^0.8.18;

import "@openzeppelin/contracts/token/ERC20/ERC20.sol";

contract Custom_ERC20 is ERC20 {

    constructor(string memory _Token_Name, string memory _Token_Symbol, uint256 initialSupply) ERC20(_Token_Name, _Token_Symbol) {
        _mint(msg.sender, initialSupply);
    }

    function mint(address _to, uint256 _amount) public {
        _mint(_to, _amount);
    }

    function burn(uint256 _amount) public {
        _burn(msg.sender, _amount);
    }

    // Custom transfer function
    function customTransfer(address _to, uint256 _amount) public returns (bool) {
        require(_to != address(0),"Invalid Recevier Address");
        
        // Call the inherited transfer function
        _transfer(msg.sender, _to, _amount);
        return true;
    }
}
```

## Functions

### Constructor

```solidity
constructor(string memory _Token_Name, string memory _Token_Symbol, uint256 initialSupply)
```

- **_Token_Name**: The name of the token (e.g., "MyToken").
- **_Token_Symbol**: The symbol of the token (e.g., "MTK").
- **initialSupply**: The initial supply of tokens, minted to the contract deployer.

### `mint`

```solidity
function mint(address _to, uint256 _amount) public
```

- **_to**: The address to receive the minted tokens.
- **_amount**: The number of tokens to mint.

### `burn`

```solidity
function burn(uint256 _amount) public
```

- **_amount**: The number of tokens to burn from the caller's balance.

### `customTransfer`

```solidity
function customTransfer(address _to, uint256 _amount) public returns (bool)
```

- **_to**: The address to receive the tokens.
- **_amount**: The number of tokens to transfer.
- **Returns**: `true` if the transfer is successful.

## Deployment

To deploy the contract, you will need the following:

- **Solidity version**: `^0.8.18`
- **Dependencies**: OpenZeppelin Contracts

### Example Deployment

1. **Initialize the contract with your desired parameters**:
   ```solidity
   Custom_ERC20 myToken = new Custom_ERC20("MyToken", "MTK", 1000000 * 10**18);
   ```
   This deploys the contract with the token name "MyToken", symbol "MTK", and an initial supply of 1,000,000 tokens.

2. **Mint additional tokens**:
   ```solidity
   myToken.mint(0xYourAddress, 5000 * 10**18);
   ```

3. **Burn tokens**:
   ```solidity
   myToken.burn(1000 * 10**18);
   ```

4. **Use the custom transfer function**:
   ```solidity
   myToken.customTransfer(0xReceiverAddress, 100 * 10**18);
   ```


This README file should provide a clear overview of the contract, its functionalities, and how to use it effectively.
