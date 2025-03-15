# ERC-20 Token Implementations

This repository contains two different implementations of ERC-20 tokens, demonstrating different approaches to token creation using Solidity and the Foundry framework.

## Overview

1. **ManualToken**: A basic ERC-20 token implementation with manual state management
2. **OurToken**: An OpenZeppelin-based ERC-20 token implementation with additional features

## Technical Specifications

### ManualToken
- **Name:** Manual Token
- **Total Supply:** 100 tokens
- **Decimals:** 18
- **Features:**
  - Manual balance tracking
  - Basic transfer functionality
  - Balance consistency checks
  - Pure view functions for token information

### OurToken
- **Name:** OurToken
- **Symbol:** OT
- **Initial Supply:** 1000 tokens
- **Features:**
  - OpenZeppelin ERC20 standard implementation
  - Standard approve/transferFrom functionality
  - Safe math operations
  - Inherits battle-tested OpenZeppelin security features

## Smart Contract Features

### ManualToken Core Functions

1. `name()`: Returns the token name
   - Pure function
   - Returns: "Manual Token"

2. `totalSupply()`: Returns the fixed total supply
   - Pure function
   - Returns: 100 ether (100 * 10^18 tokens)

3. `decimals()`: Returns the number of decimals
   - Pure function
   - Returns: 18

4. `balanceOf(address _owner)`: Queries the balance of a specific address
   - View function
   - Parameters:
     - `_owner`: Address to query
   - Returns: Current balance of the address

5. `transfer(address _to, uint256 _amount)`: Transfers tokens between addresses
   - State-modifying function
   - Parameters:
     - `_to`: Recipient address
     - `_amount`: Amount of tokens to transfer
   - Includes balance verification for security

### OurToken Core Functions

1. Standard ERC20 Functions:
   - `transfer(address to, uint256 amount)`
   - `approve(address spender, uint256 amount)`
   - `transferFrom(address from, address to, uint256 amount)`
   - `balanceOf(address account)`
   - `allowance(address owner, address spender)`

2. Constructor:
   - Initializes token with name "OurToken" and symbol "OT"
   - Mints initial supply to deployer

## Testing

The project includes comprehensive test suites for both token implementations:

### OurToken Tests (`test/OurTokenTest.t.sol`)
1. Initial Setup Test
   - Deploys token
   - Sets up test accounts (bob, alice)
   - Initializes with starting balance

2. Balance Tests
   - `testBobBalance`: Verifies correct initial balance assignment
   - `testTransfer`: Validates basic transfer functionality

3. Allowance Tests
   - `testAllowancesWorks`: Tests approve and transferFrom mechanics
   - Verifies correct balance updates after transfers

### Test Coverage
- Basic token operations
- Transfer mechanics
- Allowance functionality
- Edge cases and security checks

## Deployment

### Deployment Scripts

1. OurToken Deployment (`script/DeployOurToken.s.sol`):
```solidity
contract DeployOurToken is Script {
    uint256 public constant INITIAL_SUPPLY = 1000 ether;
    
    function run() external returns (OurToken) {
        vm.startBroadcast();
        OurToken ot = new OurToken(INITIAL_SUPPLY);
        vm.stopBroadcast();
        return ot;
    }
}
```

### Deployment Instructions

1. Install dependencies:
```bash
forge install
```

2. Build the project:
```bash
forge build
```

3. Deploy to local network:
```bash
forge script script/DeployOurToken.s.sol --rpc-url localhost
```

4. Deploy to testnet (Sepolia):
```bash
forge script script/DeployOurToken.s.sol --rpc-url $SEPOLIA_RPC_URL --private-key $PRIVATE_KEY --broadcast
```

## Security Features

- Private state variables to prevent direct manipulation
- Balance consistency checks
- Built on Solidity 0.8.18+ for automatic overflow protection
- OpenZeppelin security features (in OurToken)
- Implementation of checks-effects-interactions pattern

## Development Setup

### Prerequisites

- [Foundry](https://book.getfoundry.sh/getting-started/installation.html)
- Solidity ^0.8.18
- Git

### Installation

1. Clone the repository
```bash
git clone <your-repo-url>
cd foundry-erc20-f24
```

2. Install dependencies
```bash
forge install
```

3. Build the project
```bash
forge build
```

4. Run tests
```bash
forge test
```

## Contributing

Contributions are welcome! Please feel free to submit a Pull Request.

## License

This project is licensed under the MIT License - see the [LICENSE](LICENSE) file for details.

## Disclaimer

These implementations are for educational purposes. For production use, consider using established token standards and audited implementations.

