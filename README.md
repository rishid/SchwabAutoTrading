# SchwabAutoTrading (SAT)
We automatically trade options via some simple algorithms and it's only applicable for Charles Schwab Accounts. 
The author is Lin with MathPhdTrading and she explains her algorithms more in details in 
her Youtube Channel: https://youtube.com/@mathphdtrading-sv2024?si=3MZf12bxZ4E5TL3x. 
## Brief Description of the Algorithms
First we only sell puts and/or calls since I am a big believer of Theta trading. 
So if you are an option buyers, you can stop here. 
### How to STO a new put/call?
The new put trade has the expiration date 4 weeks out, the delta between [-0.24, -0.16] and the premium > 0.01 x strike price;
### Winning Trade?
If an existing trade has a gain > 50% and abs(delta) <= 0.14. 
We close this existing trade and open a new trade based on above.
### Losing Trade?
if an existing trade has the external value < 0.005 x strike price and expires in two weeks.
We close this existing trade, and STO a new trade that has at least 2% lower strike price and $0.30 higher premium. 

### STO tickers that have large day/week/month change
We do this based on two benefits:
1. when a stock moves down significantly, the implied volatility (IV) of the stock increases, therefore a good candidate to sell puts;
2. when a stock moves down significantly, we assume it won't go down too much, kinda like conditional probability. But don't trust this fully because some stocks go down for a reason (bad earning result, bad news). If that's the case, don't sell puts.

### Sell earning trades
IV of the stock is large!

## Installation

Before you follow the instruction below, you need to apply for a developer account from Schwab and then 
follow the instruction from Tyler Bowers's github code. Tyler Bower is the author of schwabdev, the Schwab API.
The code link is: https://github.com/tylerebowers/Schwab-API-Python
After you get your connection to Schwab account working, you should also put your APP key and APP secret to 
the Config class in configs/config.py.

If you want to do earnings trade, you should apply for an account from apicalls.io and then subscribe to the cheapest plan (currently is $0 per month). You can get 500 calls per month that include only stocks, not option data. But earning calendars are covered. The good news is you are covered for 2024 Q3 since I have all the earning tickers in data/earnings_calendar.json. 

Note: Always work under SchwabAutoTrading/, or the same level as README.md.
Use the package manager [pip](https://pip.pypa.io/en/stable/) to install.

You need to be in virtual environment to use pip. The following command creates a virtual environment .myenv in
the current directory. You only run this when it is the first time to create a virtual environment.

```bash
python3 -m venv .myenv
```

And then activate it:

```bash
source .myenv/bin/activate
```

You may wish to deactivate it later by simply typing

```bash
deactivate
```

in your shell.
When it is your first time to create a virtual environment, you need to install the necessary
libraries before running the main file, you run:
```bash
pip3 install -r requirements.txt
```

Last, don't forget to add your python path in your .bashrc.

## Code Structure
Except test/ and data/, there are main.py plus 3 folders: configs, options and trading_algorithms. 
configs: stores all the constants and enum classes. This is where you should change your app 
key, app secret and account numbers. If you have different likings of expiration date and delta, you can 
change your STO_TRADING_SETTINGS. Ideally, after you modify all the necessary variables in configs.py, 
you can just run ```python3 main.py``` every day to trade. 

options: composed of basic classes like stocks, options and option_chains. 

trading: it deals with trading current positions of all accounts in trade_options.py; and it scan 
through a list of stocks and trade it if there are significant price changes. 

main.py: Run this every day to trade!!!!

## Note
If you have any questions about the code, please email me at MathPhdTrading@gmail.com. 
