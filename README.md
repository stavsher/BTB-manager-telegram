# Binance Trade Bot Manager Telegram

A Telegram bot for remotely managing [Binance Trade Bot].

**If you have feature requests please open an issue on this repo, developers are also welcome to contribute!**

## About

I wanted to develop an easy way of managing [Binance Trade Bot] so that I wouldn't have to constantly ssh into my VPS, and my non-techy friends could enjoy the benefits of automated trading.

As of now the bot is able to perform the following actions:

- Check bot status (running / not running)
- Start _Binance Trade Bot_
- Stop _Binance Trade Bot_
- Display current coin stats (balance, USD value, BTC value, initial buying price)
- Display current coin ratios
- Display progress (how much more of a certain coin you gained since you started using _Binance Trade Bot_)
- Display trade history
- Display last 4000 characters of log file
- Edit coin list (`supported_coin_list` file)
- Edit user configuration (`user.cfg` file)
- Delete database file (`crypto_trading.db` file)
- Export database file
- **Update** _Binance Trade Bot_ (and notify when new update is available)
- **Update** _Binance Trade Bot Manager Telegram_ (and notify when new update is available)

The program's default behavior fetches Telegram `token` and `user_id` from [Binance Trade Bot]'s `apprise.yml` file.  
Only the Telegram user with `user_id` equal to the one set in the `apprise.yml` file will be able to use the bot.

⚠ The program is fully compatible with **Linux** and **Windows** through **[WSL]**, further compatibility testing needs to be done for **native Windows** and **MacOS**.

## Installation

_Python 3_ is required.  
**BTB-manager-telegram** should be installed in the same parent directory as _Binance Trade Bot_.  
Your filesystem should look like this:

```
.
└── *parent_dir*
    ├── BTB-manager-telegram
    └── binance-trade-bot
```

1. Clone this repository:

```console
$ git clone https://github.com/lorcalhost/BTB-manager-telegram.git
```

2. Move to `BTB-manager-telegram`'s directory:

```console
$ cd BTB-manager-telegram
```

3. Install `BTB-manager-telegram`'s dependencies:

```console
$ python3 -m pip install -r requirements.txt
```

⚠ Make sure the correct `rwx` permissions are set and the program is run with correct privileges.

## Usage

**BTBManagerTelegram** can be run directly by executing the following command:

```console
# Run normally
$ python3 -m btb_manager_telegram

# Run inside a docker container
$ python3 -m btb_manager_telegram --docker

# If the bot is running on a server you may want to keep it running even after ssh connection is closed by using nohup
$ nohup python3 -m btb_manager_telegram &
```

Make sure [Binance Trade Bot]'s `apprise.yml` file is correctly setup before running.  
</br>
Note:  
If _Binance Trade Bot_ and _BTB-Manager-Telegram_ were **not** installed in the same parent directory or you want to use different `token` and `user_id` from the ones in the `apprise.yml` file, the following optional arguments can be used:

```console
optional arguments:
  -p PATH, --path PATH  (optional) binance-trade-bot installation absolute path
  -t TOKEN, --token TOKEN
                        (optional) Telegram bot token
  -u USER_ID, --user_id USER_ID
                        (optional) Telegram user id
  -d DOCKER, --docker DOCKER
                        (optional) Run the script in a docker container.
                        NOTE: Run the 'docker_setup.py' file before passing this flag.
```

## Interaction

Interaction with **BTBManagerTelegram** can be _started_ by sending the `/start` command in the bot's Telegram chat.  
Every time the Telegram bot is restarted the `/start` command should be sent again.

## Screenshots

<details><summary>CLICK ME</summary>

<p align="center">
  	<img height="20%" width="20%" src="https://i.imgur.com/znI3G3H.jpg" />&nbsp;&nbsp;&nbsp;&nbsp;
    <img height="20%" width="20%" src="https://i.imgur.com/c2m0xuk.jpg" />
</p>
</details>
</br>

## Troubleshooting

### 1. I am sending the `/start` command to the bot but it's not answering:

<details><summary>CLICK ME</summary>

<p align="center">

Usually when this happens it means that you haven't properly setup your `apprise.yml` file.  
For security reasons the bot is programmed so that it only responds to the person with `user_id` equal to the one set in the Telegram URL inside the `apprise.yml` file.

Example of `apprise.yml` file:

```yaml
version: 1
urls:
  - tgram://123456789:AABx8iXjE5C-vG4SDhf6ARgdFgxYxhuHb4A/606743502
```

In this URL:

- `123456789:AABx8iXjE5C-vG4SDhf6ARgdFgxYxhuHb4A` is the bot's `token`
- `606743502` is the `user_id`

You can find your `user_id` by sending a Telegram message to [@userinfobot](https://t.me/userinfobot).

Note:  
If the bot is not responsive after using the _Update Telegram Bot_ function something might have gone wrong and you need to manually restart _BTB Manager Telegram_.

</p>
</details>
</br>

### 2. ERROR: `Make sure that only one bot instance is running`:

<details><summary>CLICK ME</summary>

<p align="center">

This means that there are two or more instances of `BTB-Manager-Telegram` running at the same time on the same Telegram `token`.  
To fix this error you can kill all `BTB-Manager-Telegram` instances and restart the Telegram bot.  
You can kill the processes using the following command:

```bash
kill -9 $(ps ax | grep btb_manager_telegram | fgrep -v grep | awk '{ print $1 }')
```

</p>
</details>
</br>

## Support the Project

<a href="https://www.buymeacoffee.com/lorcalhost"><img src="https://img.buymeacoffee.com/button-api/?text=Buy me a beer&emoji=🍺&slug=lorcalhost&button_colour=FFDD00&font_colour=000000&font_family=Lato&outline_colour=000000&coffee_colour=ffffff"></a>

## Disclaimer

This project is for informational purposes only. You should not consider any
such information or other material as legal, tax, investment, financial, or
other advice. Nothing contained here constitutes a solicitation, recommendation,
endorsement, or offer by me or any third party service provider to buy or sell
any securities or other financial instruments in this or in any other
jurisdiction in which such solicitation or offer would be unlawful under the
securities laws of such jurisdiction.

If you plan to use real money, USE AT YOUR OWN RISK.

Under no circumstances will I or the project's maintainers be held responsible or liable in any way for any claims,
damages, losses, expenses, costs, or liabilities whatsoever, including, without limitation, any direct or indirect
damages for loss of profits.

##### ⚙ Developed for love of task automation by [Lorenzo Callegari](https://github.com/lorcalhost)

[binance trade bot]: https://github.com/edeng23/binance-trade-bot
[wsl]: https://docs.microsoft.com/en-us/windows/wsl/install-win10
