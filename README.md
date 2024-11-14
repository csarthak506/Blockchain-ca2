// SPDX-License-Identifier: MIT
pragma solidity ^0.8.0;

/// @title DWG Contract
/// @dev A simple contract allowing users to deposit, withdraw, and check their Ether balance
contract DWG {
    
    // Mapping to store each address's balance
    mapping(address => uint256) private balances;

    /// @notice Deposits Ether into the contract
    /// @dev The payable modifier allows this function to receive Ether
    /// The amount sent with the transaction is added to the sender's balance
    function deposit() public payable {
        balances[msg.sender] += msg.value;
    }

    /// @notice Withdraws a specified amount of Ether from the user's balance
    /// @param amount The amount of Ether to withdraw
    /// @dev Checks if the user has enough balance before proceeding
    /// If the balance is sufficient, it deducts the amount and transfers it to the user
    function withdraw(uint256 amount) public {
        uint256 balance = balances[msg.sender];
        require(balance >= amount, "Insufficient balance"); // Ensure the user has enough balance
        balances[msg.sender] -= amount; // Deduct amount from the user's balance
        payable(msg.sender).transfer(amount); // Transfer the amount to the user
    }

    /// @notice Returns the balance of the calling address
    /// @return The balance of the caller
    function getBalance() public view returns (uint256) {
        return balances[msg.sender];
    }
}
