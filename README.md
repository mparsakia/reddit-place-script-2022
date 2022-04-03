# Reddit Place Script 2022 for UCLA
https://discord.gg/dggcbhfU

[![Code style: black](https://img.shields.io/badge/code%20style-black-000000.svg)](https://github.com/psf/black)

# Thank you jc65536 (https://github.com/jc65536/) for helping with this version.

**Message the bot channel on Discord if you have any questions regarding setup/errors.**

## About

This is a script to draw a JPG onto r/place (<https://www.reddit.com/r/place/>).

## Requirements

- [git](https://git-scm.com/book/en/v2/Getting-Started-Installing-Git)
  - Needed for the auto-pull image feature
  - Run `git --version` in the terminal to check that you have it installed
- [Python 3](https://www.python.org/downloads/)
  - Run `python3 --version` in the terminal to check that you have it installed
- [A Reddit App Client ID and App Secret Key](https://www.reddit.com/prefs/apps)

## How to Get App Client ID and App Secret Key

You need to generate an app client id and app secret key for each account in order to use this script.

Steps:

1. Visit <https://www.reddit.com/prefs/apps>
2. Click "create (another) app" button at very bottom
3. Select the "script" option and fill in the fields with anything

If you don't want to create a development app for each account, you can add each username as a developer in the developer app settings. You will need to duplicate the client ID and secret in .env, though.

![Where you will find the app client ID and secret key](reddit-app-screenshot.png)

## Clone This Project!

In your terminal, `cd` into any directory you like, then run

```
git clone https://github.com/mparsakia/reddit-place-script-2022-UCLA.git
```

Then cd into the projects root directory.

## Python Package Requirements

**Optional**
Create a virtual environment so the installed packages don't pollute your system.
This step is optional. It just helps you organize your Python packages better.

```shell
python3 -m venv env

# Linux/macOS users, run this
. env/bin/activate

# Windows users, run this
env\Scripts\activate.bat
```

Install requirements from 'requirements.txt' file.

```shell
pip3 install -r requirements.txt
```

## Get Started

Make a copy of `.env_TEMPLATE`, rename it to `.env`, and place it in the project directory.

Put in the following contents:

**Note:** The `ENV_DRAW_X_START` and `ENV_DRAW_Y_START` variables are already
configured for the UCLA flag. Do not change them.

```text
ENV_PLACE_USERNAME='["developer_username"]'
ENV_PLACE_PASSWORD='["developer_password"]'
ENV_PLACE_APP_CLIENT_ID='["app_client_id"]'
ENV_PLACE_SECRET_KEY='["app_secret_key"]'
ENV_DRAW_X_START="x_position_start_integer"
ENV_DRAW_Y_START="y_position_start_integer"
ENV_R_START='["0"]'
ENV_C_START='["0"]'
```

If you have multiple accounts (FOR UCLA):

```text
ENV_PLACE_USERNAME='["YOURUSERNAMEHERE", "redacted", "redacted", "redacted", "redacted", "redacted", "redacted", "redacted", "redacted", "redacted"]'
ENV_PLACE_PASSWORD='["YOURPASSWORDHERE", "redacted", "redacted", "redacted", "redacted", "redacted", "redacted", "redacted", "redacted", "redacted"]'
ENV_PLACE_APP_CLIENT_ID='["YOURCLIENTIDHERE", "redacted", "redacted", "redacted", "redacted", "redacted", "redacted", "redacted", "redacted", "redacted"]'
ENV_PLACE_SECRET_KEY='["SECRETKEYHERE", "redacted", "redacted", "redacted", "redacted", "redacted", "redacted", "redacted", "redacted", "redacted"]'
ENV_DRAW_X_START="357"
ENV_DRAW_Y_START="253"
ENV_R_START='["0", "0", "0", "0", "0", "0", "0", "0", "0", "0"]'
ENV_C_START='["0", "0", "0", "0", "0", "0", "0", "0", "0", "0"]'
ENV_THREAD_DELAY='30'
```

- ENV_PLACE_USERNAME is an array of usernames of developer accounts
- ENV_PLACE_PASSWORD is an array of the passwords of developer accounts
- ENV_PLACE_APP_CLIENT_ID is an array of the client ids for the app / script registered with Reddit
- ENV_PLACE_SECRET_KEY is an array of the secret keys for the app / script registered with Reddit
- ENV_DRAW_X_START specifies the x position to draw the image on the r/place canvas
- ENV_DRAW_Y_START specifies the y position to draw the image on the r/place canvas
- ENV_R_START is an array which specifies which x position of the original image to start at while drawing it
- ENV_C_START is an array which specifies which y position of the original image to start at while drawing it

### Notes:

- Multiple fields can be passed into the arrays to spawn a thread for each one.
- Change image.png/.jpg to specify what image to draw. One pixel is drawn every 5 minutes
- PNG has priority over JPG

## Run the Script

```python
python3 main.py
```

## Multiple Bots

If you want two threads drawing the image at once you could have a setup like this:

```text
ENV_PLACE_USERNAME='["developer_username_1", "developer_username_2"]'
ENV_PLACE_PASSWORD='["developer_password_1", "developer_password_2"]'
ENV_PLACE_APP_CLIENT_ID='["app_client_id_1", "app_client_id_2"]'
ENV_PLACE_SECRET_KEY='["app_secret_key_1", "app_secret_key_2"]'
ENV_DRAW_X_START="x_position_start_integer"
ENV_DRAW_Y_START="y_position_start_integer"
ENV_R_START='["0", "0"]'
ENV_C_START='["0", "50"]'
```

The same pattern can be used for multiple drawing at once. Note that the "ENV_PLACE_USERNAME", "ENV_PLACE_PASSWORD", "ENV_PLACE_APP_CLIENT_ID", "ENV_PLACE_SECRET_KEY", "ENV_R_START", and "ENV_C_START" variables MUST be string arrays of the same size.

Also note that I did the following in the above example:

```text
ENV_R_START='["0", "0"]'
ENV_C_START='["0", "50"]'
```

In this case, the first worker will start drawing from (0, 0) and the second worker will start drawing from (0, 50) from the input image.jpg file.

This is useful if you want different threads drawing different parts of the image with different accounts.

## Other Settings

```text
ENV_THREAD_DELAY='0'
ENV_UNVERIFIED_PLACE_FREQUENCY='True'
```

- ENV_THREAD_DELAY Adds a delay between starting a new thread. Can be used to spread out places over the 5-minute rate limit.
- ENV_UNVERIFIED_PLACE_FREQUENCY is for setting the pixel place frequency to the unverified account frequency (20 minutes)

- Transparency can be achieved by using the RGB value (69, 42, 0) in any part of your image
- If you'd like, you can enable Verbose Mode by adding --verbose to "python main.py". This will output a lot more information, and not neccessarily in the right order, but it is useful for development and debugging.
