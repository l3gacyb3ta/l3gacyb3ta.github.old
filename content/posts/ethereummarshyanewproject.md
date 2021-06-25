---
title: ethereum & marshy, a new project!
date: 2021-03-13
---
So a while back I was asked by my dad, _"What does BitCoin have to do with these computer parts shortages?"_ Well I knew the basics of the blockchain idea, but I didn\'t know the specifics. So after a bit of googling I found out and that was that. Now a few days later I saw a video in my YouTube recommended feed: "Programming the blockchain with Ethereum!" or something like that. I then watched it and got sucked into a rabbit hole.



After I had fallen through that, I wanted to make a smart contract. So the first thing I did was... copy an ERC20 token\'s code. (Life of a developer lol) That got me into tokens, so I found Uniswap and I was like _"I wanna make something cool and social on the blockchain! Like Uniswap!"_ So I started writing a little app to help with situations like paying a bill together with friends.



While I was writing the code for it at school (_after_ I had done my work, don\'t worry), one of my friends was looking over my shoulder and asked me what I was doing. So I explained and she really wanted to draw an icon for it, so Marshy, the bill splitting dapp, was born! (The icon is a marshmellow, fyi)



The code I\'ve written is on my [GitHub](https://github.com/l3gacyb3ta), and y\'all are free to contribute! I\'m gonna learn React to make a cool web interface using web3.js. If anyone has any tips, please contact me on my contacts page.



### Code Breakdown:



    // SPDX-License-Identifier: UNLICENSED

    pragma solidity >=0.7.0 <0.8.0;

    

    contract MarshyShare {

        // The owner, for refund of extra eth.

        address payable private owner;

        // Current eth locked up in the contract

        int256 balance;

        // The goal of the contract, once this is reached, it will pay out.

        int256 goal;

        // The address the goal should be payed out to.

        address payable payee;

    



The first bit of the code sets up the smart-contract, and gives it some properties, such as an owner, a payee, a balance, and a goal. The addresses have to be \'payable\' so that we can transfer ether to them in the future.



    // event for EVM logging

        event OwnerSet(address indexed oldOwner, address indexed newOwner);

        event GoalFulfilled();

    



This sets up a bit of logging, most of which I haven\'t implemented yet \xf0\x9f\x98\x85.



        // modifier to check if caller is owner

        modifier isOwner() {

            // If the first argument of \'require\' evaluates to \'false\', execution terminates and all

            // changes to the state and to Ether balances are reverted.

            // This used to consume all gas in old EVM versions, but not anymore.

            // It is often a good idea to use \'require\' to check if functions are called correctly.

            // As a second argument, you can also provide an explanation about what went wrong.

            require(msg.sender == owner, "Caller is not owner");

            _;

        }

    



This sets up an important \'modifier\', which can run before functions, to make sure certain functions can only be called by the owner. Nothing uses this yet, but it will come up in future Marshy versions.



        function deposit() public payable {

            // adds to balance and subracts from goal

            balance = balance + int(msg.value);

            goal = goal - int(msg.value);

    

            // If the goal is met

            if(goal <= 0) {

                // Pay the payee

                payee.transfer(uint(goal));

                // Set the new balance

                balance = balance - goal;

                // logging!

                emit GoalFulfilled();

                // transfer extra eth, if the balance is positive (should be)

                if(balance > 0){

                    owner.transfer(uint(balance));

                }

            }

        }

    



This is the big fancy deposit function! What it does is that, when ether is received, it does some math to see if the goal is met, and then pays everyone out.



        // Pretty easy, just get the balance

        function getBalance() public view returns(int256 balance) {return balance;}

    

        // Same as above, but with the current goal

        function getGoal() public view returns(int256 _goal) {return goal;}

    



These two are mostly for the web dapp I have planned, so that you can get balances and the such.



        // Fallback deposit functions

        fallback() external payable {balance = balance + int(msg.value);}

    

        receive() external payable {balance = balance + int(msg.value);}

    }

    



This is the end, and it just makes sure any accidental transfers get logged in the balance, it doesn\'t yet interact with the goal or the payout logic yet, so that\'s for an update down the line.



The full code is below, and on my GitHub. Feel free to use it, it doesn\'t have a license.



    // SPDX-License-Identifier: UNLICENSED

    pragma solidity >=0.7.0 <0.8.0;

    

    contract MarshyShare {

        // The owner, for refund of extra eth.

        address payable private owner;

        // Current eth locked up in the contract

        int256 balance;

        // The goal of the contract, once this is reached, it will pay out.

        int256 goal;

        // The address the goal should be payed out to.

        address payable payee;

    

    

        // event for EVM logging

        event OwnerSet(address indexed oldOwner, address indexed newOwner);

        event GoalFulfilled();

    

        // modifier to check if caller is owner

        modifier isOwner() {

            // If the first argument of \'require\' evaluates to \'false\', execution terminates and all

            // changes to the state and to Ether balances are reverted.

            // This used to consume all gas in old EVM versions, but not anymore.

            // It is often a good idea to use \'require\' to check if functions are called correctly.

            // As a second argument, you can also provide an explanation about what went wrong.

            require(msg.sender == owner, "Caller is not owner");

            _;

        }

    

        constructor(int256 toBePayed, address payable _payee) {

            // Set balance to 0

            balance = 0;

            // The owner is the sender and the payee is the _payee argument

            owner = msg.sender;

            payee = _payee;

            // setup goal

            goal = toBePayed;

        }

    

    

        function deposit() public payable {

            // adds to balance and subracts from goal

            balance = balance + int(msg.value);

            goal = goal - int(msg.value);

    

            // If the goal is met

            if(goal <= 0) {

                // Pay the payee

                payee.transfer(uint(goal));

                // Set the new balance

                balance = balance - goal;

                // logging!

                emit GoalFulfilled();

                // transfer extra eth, if the balance is positive (should be)

                if(balance > 0){

                    owner.transfer(uint(balance));

                }

            }

        }

    

        // Pretty easy, just get the balance

        function getBalance() public view returns(int256 balance) {return balance;}

    

        // Same as above, but with the current goal

        function getGoal() public view returns(int256 _goal) {return goal;}

    

        // Fallback deposit functions

        fallback() external payable {balance = balance + int(msg.value);}

    

        receive() external payable {balance = balance + int(msg.value);}

    }