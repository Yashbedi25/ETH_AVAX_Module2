# Function Frontend-Dapp

Create a simple contract with 2-3 functions. Then show the values of those functions in front end of the application. Make Dapp

## Description

This program is like a bank where users can deposit, withdraw, or transfer Ethereum from one metamask account to another account. 
Here I use React js for developing Dapp. This Solidity program shows you all the functions and variables required for making the Dapp.



## Getting Started

### Executing program

To run this program, I use VsCode(local Compiler) . to get started I use some of the node modules by importing them into the system locally.
Some of the commands are :
i)npx hardhat
ii)npm install --save-dev "hardhat@^2.16.1" "@nomicfoundation/hardhat-toolbox@^2.0.0"
iii)npx hardhat node
iv)npx hardhat run --network localhost scripts/deploy.js
v)npm start

```javascript
// SPDX-License-Identifier: GPL-3.0

pragma solidity >=0.7.0 <0.9.0;

contract BankApp{
    mapping (address=>uint256) UserAccount; 
    mapping (address=>bool) UserExists;
    
    function createAcc() public returns (bool)
    {
        require(UserExists[msg.sender]==false,'User already Exists'); UserExists[msg.sender]=true; return true;
    }


    function accountExists() public view returns (bool)
    {
        return UserExists[msg.sender];
    }


    function deposit() public payable
    {
        UserAccount[msg.sender] = UserAccount[msg.sender] + msg.value;
    }


    function withdraw(uint256 withdrawAmount) public payable
    {
        require( (UserExists[msg.sender]==true) && (withdrawAmount <UserAccount[msg.sender]) );
        UserAccount[msg.sender] = UserAccount[msg.sender] - withdrawAmount;
        // Now get that amount withdrawed //Amount withdrawed must be transfered payable(msg.sender).transfer(withdrawAmount);
    }



    function accountBalance() public view returns(uint256)
    {
        return UserAccount[msg.sender];
    }

 
    function transferEther(address payable reciever, uint256 transferAmount) public payable{    
        require((UserExists[reciever]== true)&&(UserExists[msg.sender]== true)&&(transferAmount>0)); require( transferAmount < UserAccount[msg.sender] );
        UserAccount[msg.sender] = UserAccount[msg.sender] - transferAmount;
        UserAccount[reciever]+= transferAmount;
        //Amount withdrawed must be transfered reciever.transfer(transferAmount);
    }
}

```
After npm start, Dapp will show on "http://localhost:3000/ " locally and all the function will perform accordingly

## Authors

Yash Bedi 
[@YashBedi_25](https://twitter.com/Yash_Bedi25)


## License

This project is licensed under the MIT License - see the LICENSE.md file for details
