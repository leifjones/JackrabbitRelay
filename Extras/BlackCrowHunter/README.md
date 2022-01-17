# Black Crow Hunter

**WORKING DRAFT**

In trading, a black crow is 3 consecutive downwards candles.
BlackCrowHunter takes this concept and extends it to allow the ability to
search for any number of downward candles. 

Simply put, the more consecutive candles in a row, the less purchases
made and the more likely the market will rebound. Fewer candles are more
aggressive and more accumulation.

## Disclaimer

Please note RAPMD Crypto, LLC ("the Company"), does not provide financial
advice. The Company, and any associated companies, owners, employees,
agents or volunteers, do not hold  themselves out as Commodity Trading
Advisors (“CTAs”) or Authorized Financial Advisors  (“AFAs”). The owners,
publishers, employees and agents are not licensed under securities laws 
to address particular investment situations. No information presented
constitutes a  recommendation to buy, sell or hold any security,
financial product or instrument discussed  therein or to engage in any
specific investment strategy.

All content is for informational purposes only. The content provided
herein is not intended to replace or serve as a substitute for any
legal, tax, investment or other professional advice,  consultation or
service. It is important to do your own analysis before making any
investment  based on your own financial circumstances, investment
objectives, risk tolerance and liquidity needs.

All investments are speculative in nature and involve substantial risk of
loss. The Company does not in any way warrant or guarantee the success of
any action you take in reliance on the  statements, recommendations or
materials. The Company, owners, publishers, employees and  agents are not
liable for any losses or damages, monetary or other that may result from
the  application of information contained within any statements,
recommendations or materials.  Individuals must use their own due
diligence in analyzing featured trading indicators, other trading  tools,
webinars and other educational materials to determine if they represent
suitable and  useable features and capabilities for the individual.

Use this Software at your own risk. It is provided AS IS. The Company
accepts no responsibility or liability for losses incurred through using
this software. While The Company has gone to great lengths to test the
software, if you do find any bugs, please report them to us in the
[Jackrabbit Support Server](https://discord.gg/g93TpbV) or on Github, and
we will sort them out. Remember that risk management is your
responsibility. If you lose your account, that's entirely on you.

Past performance is not indicative of future results. Investments involve
substantial risk. Any past  results provided are intended as examples
only and are in no way a reflection of what an individual  could have
made or lost in the same situation.

## Installation

Installation is very simple. Just follow the below:

```bash
cd /home/GitHub/JackrabbitRelay/Extras/BlackCrowHunter
./install
```

## Reboot startup

For BlackCrowHunter to auto start after a reboot, the following line
needs to be added to your crontab. 

```crontab
@reboot ( /home/BlackCrowHunter/Launcher kucoin MAIN trx/usd 5 1 1 PAPER & ) > /dev/null 2>&1
```

Please be aware that the exchange, coin, and other parameters **MUST**
match the below usage. The cronjob will only work properly when it is
aligned with a tested working coin.

You should extensively test your coin first with a virtual console
**before** setting up a cronjob.

## Configuration

BlackCrowHunter uses the same configuration as Jackrabbit Relay, *with one
very import addition*. Your configuration must have a webhook item on
each API/Secret combination the BlackCrowHunter uses.

This example is for KuCoin, but applies to *all* exchanges where
BlackCrowHunter will be used. The Webhook **MUST** be present and point to
your IP address/port entry for Jackrabbit Relay. 

**The port used below, 7732, is EXAMPLE ONLY. It MUST be changed to YOUR
installation.**

```json
# Spot Market - JackrabbitRelay
{ "Account":"MAIN","API":"API1","SECRET":"SECRET1","Passphrase":"pw1","RateLimit":"1000","Retry":"3","Webhook":"http://127.0.0.1:7732" }

# Spot Market - JackrabbitRelay1
{ "Account":"MAIN","API":"API2","SECRET":"SECRET2","Passphrase":"pw2","RateLimit":"1000","Retry":"3","Webhook":"http://127.0.0.1:7732" }

# Spot Market - JackrabbitRelay2
{ "Account":"MAIN","API":"API3","SECRET":"SECRET3","Passphrase":"pw3","RateLimit":"1000","Retry":"3","Webhook":"http://127.0.0.1:7732" }
```

BlackCrowHunter rotates your API/Secret on **EVERY** call to your exchange.
You should have *at least* **THREE (3)** API/Secret listings in your
exchange configuration that BlackCrowHunter will use.

BlackCrowHunter does not have to be on the same machine as Relay, but latency
and slippage will be a consideration otherwise, not to mention security.

## Usage

```bash
cd /home/BlackCrowHunter
./Launcher       kucoin MAIN ada/usdt  5   1   1    PAPER
```

Or, for futures trading

```bash
cd /home/BlackCrowHunter
./BlackCrowHunter.spot kucoin MAIN ada/usdt 5 1 1
```

This launches BlackCrowHunter. The arguments are as follows:

| Argument | Example   | Description |
| --- | --------- | -------------------- |
| 1 | `kucoin`   | Exchange              |
| 2 | `MAIN`     | Account (Case sensitive) |
| 3 | `ada/usdt` | Asset                |
| 4 | `5`        | Number of consecutive red or downward candles to match. The larger this number, the more defensive BlackCrowHunter will be. |
| 4 | `1`        | Deviation/Take Profit/Boundary in percent form. (`1` maps to 1%) |
| 5 | `1`        | **Number of lots to buy** <br><br> A lot is the minimum position size. If you wanted a $10 position of an asset that has a minimum position size of $2.50, you would want `4` lots. |

## Donations

If you would like to help support this project financially, please use
any of the below addresses. Anything donated goes to the costs of
sustaining Jackrabbit Relay. Thank you.

You can subscribe to the Jackrabbit Relay tier for recurring monthly
support:

    https://www.patreon.com/RD3277

If you prefer crypto or just a one time donation, please use any of the
below:
| | |
| :--- | :--- |
| BCH | bitcoincash:qzw5h5ccfz6v7zzh0vf5pl0eqp3zjmp5us07l72nvv|
| BTC | 3JUbL3Vsj61VBAmyHtQhyiFJcizEfxAvzV |
| ETH | 0x3c6C06150B2f24b3179a50b618aD3c0f58CF74FD |
| LINK | 0xd8Fd4fA3b489861ad6Eb95a0617B4DA7c78123F8 |
| LTC | MHj8nQcRdJWVVNeHUemSQgzBw3cPrZEtRU |
| USDT | 0xd8Fd4fA3b489861ad6Eb95a0617B4DA7c78123F8 |