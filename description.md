# CryptoSim Exchange

The proposed application aims to simulate a cryptocurrency exchange, where users buy and sell coins for EUR at prices set by the administrator, and derive statistics based on the trades.

# Features

## Managing the market (Admin interactions)

### Networks

---

**Add network**

The admin can register a new blockchain network with its name, short code and consensus type.

- The code must be 2 to 6 uppercase letters.
- Two networks with the same name or code cannot exist.
- The consensus type (the way the network agrees on transactions) must be either Proof of Work or Proof of Stake.
- A network cannot be deleted, because coins and past trades refer to it. If a network stops working, the admin delists its coins instead.
- Technical details of the network (blocks, network fees, wallets) will not be considered.

---

**List networks**

The admin can list all networks.

- For each network the code, the name, the consensus type, the number of active coins and the number of delisted coins on it should be shown.
- Networks without any coins should also be listed.
- The list is ordered by name.

---

### Coins

---

**Add coin**

The admin can register a new coin with its symbol, name, network and initial price.

- Symbols must be 2 to 6 uppercase letters.
- Two coins with the same symbol or the same name cannot exist.
- The network must be selected from the existing list of networks.
- Each coin belongs to exactly one network. A coin existing on several networks will not be considered.
- The initial price must be positive and is given in EUR.
- The initial price is recorded as the coin's first price, valid from the moment the coin is added.
- A newly added coin is active and can be traded immediately.

---

**Delist coin**

The admin can delist a coin that should no longer be traded.

- A delisted coin cannot be bought, but users who own it can still sell it at its last price.
- A delisted coin cannot be listed again.
- An already delisted coin cannot be delisted.

---

**List and search coins**

The admin can list coins, optionally filtered by a search string.

- If a search string is given, only coins whose symbol or name includes it as a substring are listed, ignoring upper/lower case.
- The admin can restrict the list to one network, and to only active or only delisted coins.
- For each listed coin the symbol, name, network, current price and whether it is active or delisted should be shown.

---

### Prices

---

**Set price**

The admin can set a new price for an active coin.

- The admin should be able to select the coin with searching from the active coins.
- The price must be positive and given in EUR.
- The new price is valid from the moment it is set until the next price is set.
- Prices of delisted coins cannot be changed.
- The application will not consider real markets, the price is whatever the admin enters.
- Prices change only when the admin sets them. Purchases and sales by users do not move the price.
- The application will not consider different time zones, everything will be in UTC+1, without daylight saving time.

---

## Trading (User interactions)

### Account

---

**Register**

A person can create a user account with a username.

- The username must be 3 to 20 characters long and may contain only letters, digits and underscores.
- Two users with the same username cannot exist, ignoring upper/lower case.
- A new account starts with zero EUR balance and no coins.
- There is no login and no passwords. After starting the application, the person picks their account from the list of registered users and acts as that user.

---

**Deposit EUR**

A user can add money to their balance.

- The amount must be positive, with at most 2 decimal places.
- The payment itself is not simulated, a valid deposit always succeeds.
- Every deposit is recorded with its date & time.

---

**Withdraw EUR**

A user can take money out of their balance.

- The amount must be positive, with at most 2 decimal places.
- The amount must not be more than the current balance, otherwise the withdrawal fails and nothing changes.
- Every withdrawal is recorded with its date & time.

---

### Trading

---

**Buy coin**

A user can buy a given amount of an active coin at its current price.

- The user should be able to select the coin with searching from the active coins.
- The amount must be positive and may be fractional, with at most 8 decimal places.
- The total cost is the amount multiplied by the current price, rounded to 2 decimal places (half up). If it is more than the user's EUR balance, the purchase fails.
- The exchange itself is the seller in every purchase, and it is assumed to always have enough coins. Users do not trade with each other, so there is no waiting for a matching seller.
- The price used is stored with the purchase, so later price changes do not affect it.
- There are no fees.

---

**Sell coin**

A user can sell a given amount of a coin they own at its current price.

- The amount must be positive and at most the amount the user owns, otherwise the sale fails.
- The exchange itself is the buyer in every sale, and it is assumed to always have enough EUR.
- The amount multiplied by the current price, rounded to 2 decimal places (half up), is added to the user's EUR balance.
- Delisted coins can also be sold, at their last price.
- The price used is stored with the sale.
- There are no fees.

---

### Overview

---

**View portfolio**

A user can see which coins they currently own and how much they are worth.

- For each owned coin the network, the amount, the current price and the current value in EUR should be shown.
- Coins the user no longer owns should not appear.
- The EUR balance and the total value of all coins plus the EUR balance should also be shown.

---

**View transaction history**

A user can list everything they have done on their account.

- Deposits, withdrawals, purchases and sales are all listed, newest first.
- Each entry shows the date & time, the type, the coin and amount (for purchases and sales), the price used, and the change of the EUR balance.
- The user can restrict the list to a period or to one type of transaction.

---

## Analysis (Analyst interactions)

---

**Top coins by trading volume**

The analyst can list the top 5 most traded coins or networks within a given period.

- The volume of a coin is the total EUR value of all its purchases and sales in the period. The volume of a network is the sum of the volumes of its coins.
- The analyst chooses whether coins or networks are listed.
- There are three ordering criteria: by volume, by number of trades, or by number of different users who traded.
- The analyst can restrict the analysis to purchases only or to sales only.
- For each listed item the name, the volume, the number of trades and the number of different users should be shown.
- Delisted coins are also included if they were traded in the period.

---

**Top gainers and losers**

The analyst can list the 5 coins whose price rose the most and the 5 coins whose price fell the most within a given period.

- The change of a coin is the difference between its price at the end and at the start of the period, in percent of the starting price.
- The price of a coin at a given moment is the last price set for it before or at that moment.
- If a coin was added during the period, its initial price is used as the starting price.
- Coins added after the period or delisted before it are not considered.
- A coin can appear among the gainers only if its price went up, and among the losers only if it went down.
- The analyst can restrict the analysis to a single network.
- For each listed coin the symbol, the network, the starting price, the ending price and the change in percent should be shown.
- Only prices set by the admin are considered, trades by users do not affect the result.

---

**Biggest profits and losses**

The analyst can list the 5 users with the highest and the 5 users with the lowest realized profit.

- The realized profit of a sale is the money received minus what the sold coins cost the user, where the cost of a coin is the average price the user paid for it in all their purchases of that coin before the sale: the total EUR paid divided by the total amount bought.
- The realized profit of a user is the sum of the realized profits of all their sales.
- The analyst can restrict the analysis to one coin and/or to a period (only sales within the period count).
- Users who have never sold anything are not listed.
- For each listed user the username, the realized profit and the number of sales should be shown.
- Coins that are still held (unrealized profit) are not considered.
