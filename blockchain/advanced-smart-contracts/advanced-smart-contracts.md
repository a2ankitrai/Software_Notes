# Advanced Smart Contracts
---

## The Lottery Contract

![001_lottery_contract_1.png](./images/001_lottery_contract_1.png)

It will have a price pool and a list of people who have entered for the prize pool.

![001_lottery_contract_2.png](./images/001_lottery_contract_2.png)

The Players will pay some ether to participate in the Lottery.

![001_lottery_contract_3.png](./images/001_lottery_contract_3.png)

Another User (Manager) will initiate the Lottery contract to pick a winner

![001_lottery_contract_4.png](./images/001_lottery_contract_4.png)

The contracts will look at its list of participants it will pick one of the players and it will send all of the money out of the prize pool to that particular winner. At that point the lottery contract then resets and then becomes ready to accept a new list of players and repeat itself all over again.

So essentially it's a self repeating contract that can be used for playing a tiny little lottery.

---

## Lottery Design

![002_lottery_design_1.png](./images/002_lottery_design_1.png)

---

## Basic Solidity Types

![003_solidity_type_1.png](./images/003_solidity_type_1.png)

address type or a variable of type address is specifically meant for storing addresses.

![003_solidity_type_2.png](./images/003_solidity_type_2.png)

The number after the word int specifies the number of bits that are used to store this particular number the number of bits that are used to store a number will specify exactly how large a number this variable can contain. Same for `uint`.

![003_solidity_type_3.png](./images/003_solidity_type_3.png)


We usually do not end up doing a lot of math inside of our contracts. Remember these contracts are way more about storing raw data and implementing some simple very simple business logic.

As soon as we start doing complex math remember we pay for every operation that occurs inside of our contract. So it just ever happens that as we're writing these contracts, we very rarely end up putting some really critical business logic or some really complex math because we don't have to pay for doing that math.

---























----
