# Please read!


**For any problems running this specific bot:** [Discord Project Post](https://discord.com/channels/974519864045756446/1055336272543092757)

**For general OpenAI API problems or questions:** [Discord API Discussions](https://discord.com/channels/974519864045756446/1037561178286739466)

**For bugs in the template code:** create an Issue

**For feature requests:** this repo is not accepting feature requests, you can discuss potential features in [Discord Project Post](https://discord.com/channels/974519864045756446/1055336272543092757)

**For PRs:** only bug fix PRs wil be accepted. If you are implementing a new feature, please fork this repo.

Thank you!

---
# GPT Discord Bot

Example Discord bot written in Python that uses the [completions API](https://beta.openai.com/docs/api-reference/completions) to have conversations with the `gpt-3.5-turbo` or `gpt-4` models.

This bot uses the [OpenAI Python Library](https://github.com/openai/openai-python) and [discord.py](https://discordpy.readthedocs.io/).


# Features

- `/chat` starts a public thread, with a `message` argument which is the first user message passed to the bot
- The model will generate a reply for every user message in any threads started with `/chat`
- The entire thread will be passed to the model for each request, so the model will remember previous messages in the thread
- when the context limit is reached, or a max message count is reached in the thread, bot will close the thread
- you can customize the bot instructions by modifying `config.yaml`
- you can change the model, the hardcoded value is `text-davinci-003`

# Setup

1. Copy `.env.example` to `.env` and start filling in the values as detailed below
1. Go to https://beta.openai.com/account/api-keys, create a new API key, and fill in `OPENAI_API_KEY`
1. Create your own Discord application at https://discord.com/developers/applications
1. Go to the Bot tab and click "Add Bot"
    - Click "Reset Token" and fill in `DISCORD_BOT_TOKEN`
    - Disable "Public Bot" unless you want your bot to be visible to everyone
    - Enable "Message Content Intent" under "Privileged Gateway Intents"
1. Go to the OAuth2 tab, copy your "Client ID", and fill in `DISCORD_CLIENT_ID`
1. Copy the ID the server you want to allow your bot to be used in by right clicking the server icon and clicking "Copy ID". Fill in `ALLOWED_SERVER_IDS`. If you want to allow multiple servers, separate the IDs by "," like `server_id_1,server_id_2`
1. Install dependencies and run the bot
    ```
    pip install -r requirements.txt
    python -m src.main
    ```
    You should see an invite URL in the console. Copy and paste it into your browser to add the bot to your server.
    Note: make sure you are using Python 3.9+ (check with python --version)

# Optional configuration

- If you want to change the model used, you can do so in `OPENAI_MODEL`. Currently only `gpt-3.5-turbo` and `gpt-4` work with the present codebase.

- If you want to change the behavior/personality of the bot, change the system prompt in `SYSTEM_MESSAGE`, with optional variables enclosed in `{`curly braces`}`. Currently the only variables available are `current_date` and `knowledge_cutoff`, with the latter being equivalent to the environment variable of the same name. The former is always in ISO 8601 format.

# FAQ

> Why isn't my bot responding to commands?

Ensure that the channels your bots have access to allow the bot to have these permissions.
- Send Messages
- Send Messages in Threads
- Create Public Threads
- Manage Messages (only for moderation to delete blocked messages)
- Manage Threads
- Read Message History
- Use Application Commands
