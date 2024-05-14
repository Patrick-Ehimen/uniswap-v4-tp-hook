# Uniswap v4 Take Profits Hook

## Overview

This project demonstrates the implementation of a "take-profit" orders hook for Uniswap v4. The hook allows users to place on-chain take-profit orders, where they can specify the exact price at which they want to close their position and receive the swapped tokens.

The key features of this take-profits hook are:

1. **Placing Take-Profit Orders**: Users can place take-profit orders by specifying the trading pool, target tick (price), and the amount of tokens they want to swap.
2. **Canceling Orders**: Users can cancel their placed take-profit orders if they no longer want to execute them.
3. **Automatic Order Execution**: The hook's main logic is in the `afterSwap` function, which checks if any placed take-profit orders can be fulfilled based on the new price after a swap. If so, it executes the order and the user can then claim the swapped tokens.
4. **ERC-1155 Token Integration**: The hook uses ERC-1155 tokens as a "receipt" to represent the placed take-profit orders. Users can return these tokens to the hook to withdraw their swapped tokens.

## Setup

### Prerequisites

- Foundry installed on your system
- Familiarity with Solidity and Uniswap v4 concepts

### Installation

1. Clone the repository:

```
git clone https://github.com/Patrick-Ehimen/uniswap-v4-tp-hook.git
```

2. Change to the project directory:

```
cd uniswap-v4-take-profits
```

3. Install dependencies:

```
forge install
```

## Usage

### Compiling the Contracts

To compile the contracts, run:

```
forge build
```

### Running Tests

To run the Foundry tests, execute:

```
forge test
```

The test suite includes the following tests:

1. `test_placeOrder`: Ensures that users can place take-profit orders correctly.
2. `test_cancelOrder`: Verifies that users can cancel their placed take-profit orders.
3. `test_orderExecute_zeroForOne`: Tests the execution of a take-profit order in the zeroForOne direction (selling Token 0 for Token 1).
4. `test_orderExecute_oneForZero`: Tests the execution of a take-profit order in the oneForZero direction (selling Token 1 for Token 0).
5. `test_multiple_orderExecute_zeroForOne`: Ensures that when multiple take-profit orders are placed, the hook correctly executes the orders in the right order as the price changes.

### Deploying the Hook

To deploy the take-profits hook to a Uniswap v4 environment, you will need to:

1. Deploy the `TakeProfitsHook` contract.
2. Ensure that the hook's address follows the required pattern for Uniswap v4 hooks (using `CREATE2` if necessary).
3. Register the hook with the Uniswap v4 PoolManager contract.

## Contributing

If you find any issues or have suggestions for improvements, please feel free to open an issue or submit a pull request.

## License

This project is licensed under the [MIT License](LICENSE).
