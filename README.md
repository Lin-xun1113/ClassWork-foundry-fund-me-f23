# FundMe Smart Contract Project

This is a crowdfunding smart contract project developed with Foundry as a follow-along assignment for a Solidity course. The project implements a simple crowdfunding functionality that allows users to send ETH to the contract, with only the contract owner being able to withdraw these funds.

## Project Overview

The FundMe contract is a simple crowdfunding platform with the following features:

- Users can fund the project by sending ETH (minimum amount is ETH equivalent to 5 USD)
- The contract uses Chainlink Oracle to get real-time ETH/USD price
- Only the contract owner can withdraw all funds
- Implements two withdrawal methods, with `cheaperWithdraw` optimizing memory usage to reduce gas costs

## Tech Stack

- **Solidity**: Smart contract programming language
- **Foundry**: Ethereum development toolkit
  - **Forge**: Testing framework
  - **Anvil**: Local Ethereum node
  - **Cast**: Tool for interacting with EVM smart contracts
- **Chainlink**: Oracle used for obtaining ETH/USD price data

## Project Structure

```
foundry-fund-me-f23/
├── src/                    # Source code
│   ├── FundMe.sol          # Main contract
│   └── PriceConverter.sol  # Price conversion library
├── script/                 # Deployment and interaction scripts
│   ├── DeployFundMe.s.sol  # Deployment script
│   ├── HelperConfig.s.sol  # Network configuration helper
│   └── Interactions.s.sol  # Contract interaction scripts
├── test/                   # Test files
│   ├── integration/        # Integration tests
│   ├── mocks/              # Mock contracts
│   └── uint/               # Unit tests
└── foundry.toml            # Foundry configuration file
```

## Core Contracts

### FundMe.sol

This is the main contract of the project, implementing crowdfunding functionality:

- `fund()`: Allows users to send ETH to the contract
- `withdraw()`: Allows the owner to withdraw all funds
- `cheaperWithdraw()`: Optimized withdrawal method to reduce gas costs

### PriceConverter.sol

This is a library contract used for:

- Getting ETH/USD price from Chainlink Oracle
- Converting ETH amounts to their USD equivalent

## Installation and Setup

1. Clone the repository

```bash
git clone <repository-url>
cd foundry-fund-me-f23
```

2. Install dependencies

```bash
forge install
```

3. Compile contracts

```bash
forge build
```

## Testing

The project includes unit tests and integration tests:

```bash
# Run all tests
forge test

# Run specific test
forge test --match-test testFundFailsWithoutEnoughETH

# View test coverage
forge coverage
```

## Deployment

### Local Deployment

1. Start a local node

```bash
anvil
```

2. Deploy the contract

```bash
forge script script/DeployFundMe.s.sol --rpc-url http://localhost:8545 --private-key 0xac0974bec39a17e36ba4a6b4d238ff944bacb478cbed5efcae784d7bf4f2ff80 --broadcast
```

### Testnet Deployment

Deploy to Sepolia testnet:

```bash
forge script script/DeployFundMe.s.sol --rpc-url $SEPOLIA_RPC_URL --private-key $PRIVATE_KEY --broadcast --verify --etherscan-api-key $ETHERSCAN_API_KEY
```

## Interacting with the Contract

After deployment, you can interact with the contract using the following scripts:

```bash
# Send funds to the contract
forge script script/Interactions.s.sol:FundFundMe --rpc-url $RPC_URL --private-key $PRIVATE_KEY --broadcast

# Withdraw funds from the contract
forge script script/Interactions.s.sol:WithdrawFundMe --rpc-url $RPC_URL --private-key $PRIVATE_KEY --broadcast
```

## License

MIT

## Acknowledgements

- Thanks to Patrick Collins for guidance through his Solidity course
- Thanks to Chainlink for providing price oracle services
