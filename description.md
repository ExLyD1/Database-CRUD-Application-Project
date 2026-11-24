# CryptoSim Exchange

The proposed application simulates a cryptocurrency exchange without real money. Users hold a balance in EUR, and can buy and sell coins (such as BTC or ETH) at the price currently listed by the exchange. Based on the recorded trades, analysts can derive statistics about the market.

A few concepts are worth knowing:

- A **coin** is a tradable crypto asset, identified by a short symbol (e.g., BTC).
- A **price** is the value of one coin in EUR at a given moment. There is no real market: the administrator sets prices by hand, and each price is valid from the moment it is set until the next one is set.
- A **portfolio** is the amount of each coin a user currently owns.
- A **trade** is a purchase or sale of a coin at the current price. There are no orders waiting for a matching counterpart: a trade is executed immediately against the exchange.
- **Realized profit** of a user on a coin is what they earned from sales minus what they paid for the coins they sold.

# Features

## Managing the market (Admin interactions)

### Coins

---

**Add coin**

The admin can register a new coin with its symbol, name and initial price.

- Symbols must be 2 to 6 uppercase letters.
- Two coins with the same symbol or the same name cannot exist.
- The initial price must be positive, and is valid from the moment of registration.
- A newly added coin is active and can be traded immediately.

---

**Delist coin**

The admin can delist a coin that should no longer be traded.

- A delisted coin cannot be bought, but can still be sold by users who own it, at its last listed price.
- A delisted coin cannot be listed again.
- An already delisted coin cannot be delisted.

---

**List coins**

The admin can list all coins.

- For each coin the symbol, name, current price and whether it is active or delisted are shown.
- The admin can choose to show only active coins or only delisted ones.

---

**Search among coins**

The admin can search for coins.

- All coins whose symbol or name includes the provided string as a substring are listed, ignoring upper/lower case.
- The same details as in the listing above are shown for each result.

---

### Prices

---

**Set price**

The admin can set a new price for an active coin.

- The price must be positive and given in EUR.
- The new price is valid from the moment it is set, until the next price is set.
- Prices of delisted coins cannot be changed.
- The application does not take external markets into account: the price is whatever the admin enters.
- Everything is assumed to be in one time zone (UTC+1), without daylight saving time.

---

**View price history**

The admin can view the past prices of a coin within a given period.

- The admin selects the coin by searching among the coins.
- Each entry shows the price and the moment from which it was valid.
- The list is ordered from newest to oldest.
- For the selected period, the highest and the lowest price are also shown.

---

## Trading (User interactions)

### Account

---

**Register**

A person can create a user account with a username and an email address.

- Usernames and email addresses must be unique.
- A new account starts with an empty balance and an empty portfolio.
- Authentication (passwords) is not considered. The user simply selects the account to work with.

---

**Deposit EUR**

A user can add money to their balance.

- The amount must be positive.
- The payment itself is not simulated: the deposit always succeeds if the amount is valid.
- Every deposit is recorded with its time.

---

**Withdraw EUR**

A user can take money out of their balance.

- The amount must be positive and at most the current balance, otherwise the operation fails and nothing changes.
- Every withdrawal is recorded with its time.

---

### Trading

---

**Buy coin**

A user can buy a given amount of an active coin at its current price.

- The coin is selected by searching among the active coins.
- The amount can be fractional, with up to 8 decimal places, and must be positive.
- The total cost is amount × current price. If it exceeds the user's EUR balance, the purchase fails.
- On success the balance decreases by the total cost, and the coins are added to the portfolio.
- The price used is stored with the trade, so it is not affected by later price changes.
- There are no fees.

---

**Sell coin**

A user can sell a given amount of a coin they own at its current price.

- The amount must be positive and at most the amount the user owns, otherwise the sale fails.
- On success the coins are removed from the portfolio, and amount × current price is added to the balance.
- Delisted coins can also be sold, at their last listed price.
- The price used is stored with the trade.
- There are no fees.

---

### Overview

---

**View portfolio**

A user can see what they currently own.

- For each owned coin the amount, the current price and the current value in EUR are shown.
- Coins with zero amount are not shown.
- The total value of the portfolio plus the EUR balance is also shown.

---

**View transaction history**

A user can see everything they have done on their account.

- Deposits, withdrawals, purchases and sales are all included, newest first.
- Each entry shows the time, the type, the coin and amount (for trades), the price used and the change in EUR balance.
- The user can restrict the list to a time period or to a single type of transaction.

---

## Analysis (Analyst interactions)

---

**Top coins by trading volume**

The analyst can list the 5 most traded coins in a chosen period.

- The volume of a coin is the sum of amount × price over all its trades (both purchases and sales) in the period.
- The analyst can instead order by the number of trades, or by the number of different users who traded the coin.
- The analyst can restrict the analysis to purchases only or to sales only.
- For each listed coin the symbol, the volume, the number of trades and the number of different users are shown.
- Delisted coins are included if they were traded in the period.

---

**Most active hours**

The analyst can see at which hours of the day the exchange is the busiest.

- The day is divided into 24 one-hour slots, and every trade in the chosen period is counted in the slot of its time.
- The 5 busiest slots are listed with their number of trades and total volume in EUR.
- The analyst can select a single coin to see the slots for that coin only.
- For each listed slot, the most traded coin in that slot is also shown.
- Only trades are considered, not deposits and withdrawals.

---

**Biggest profits and losses**

The analyst can list the users with the highest and lowest realized profit.

- The realized profit of a user is the sum they received from sales minus the cost of the coins sold, where the cost of a coin is the average price the user paid for it over all their purchases of that coin up to the moment of the sale.
- The top 5 users with the highest profit and the 5 with the lowest (possibly negative) profit are listed.
- The analyst can restrict the analysis to one coin and/or to a time period (only sales in the period count).
- Users who never sold anything are not listed.
- For each listed user the username, the realized profit and the number of sales are shown.
- Unrealized profit (coins still held) is not considered.
