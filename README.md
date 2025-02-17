Prerequisites

Go Installed: Ensure you have Go installed on your machine.

Telegram Account: You need a Telegram account to create a bot.

How to Create a Telegram Bot
1. Create a Bot with BotFather:
Open Telegram and search for BotFather (an official Telegram bot).
Start a chat with BotFather and type /start.
Create a new bot by typing /newbot.
2. Set a Bot Name and Username:
Bot Name: This will be the display name for your bot (e.g., My Awesome Bot).
Username: This must be unique and end with bot (e.g., my_awesome_bot).
3. Get Your Bot Token:
Once the bot is created, BotFather will provide a token.
Example token: 123456789:ABCDEFghijklMNOpQRstuvwxYZ1234567890
Copy this token. You'll use it in the Go script to authenticate the bot.
4. Start the Bot:
Open the bot by searching for its username in Telegram and send a message (e.g., "Hello").

How to Use the Go Script
1. Clone the Repository (or create a .go file):
Copy the script into a file named fetch_chat_ids.go.
2. Install Go (if not installed):
Follow the instructions to install Go: Go Installation.
3. Replace the Token:
Open the Go script (fetch_chat_ids.go).
Replace the placeholder YOUR_BOT_TOKEN with the token you received from BotFather.
Example:
const token = "123456789:ABCDEFghijklMNOpQRstuvwxYZ1234567890"
4. Run the Go Script:
Open a terminal or command prompt in the directory where the fetch_telegram_id.go file is located.

Run the following command:

go run fetch_telegram_id.go
The script will print out the user chat ID, group chat ID, and channel chat ID for any interactions the bot has received. It will also display usernames and titles for groups and channels.

Notes

The bot must have received at least one message (or be in a group/channel) to fetch the chat IDs.
If no messages are found, the script will output: 

No user messages found, No group messages found, or No channel posts found.

If you're working with a private group or channel, ensure your bot has been added to it.
