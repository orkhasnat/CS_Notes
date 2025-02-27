`discord.py` is a popular Python library for creating Discord bots.

### Installation
```bash
pip install discord.py
```

### Set a bot up
1. To use the api, we need to register a bot through the discord developer portal [Portal link](https://discord.com/developers/applications). 
2. Create a new app and add a bot
3. **Remember to carefully store the `TOKEN`.**
4. In the OAuth2 tab, add the scope **(Only choose `bot`)**
5. Tick all bot permissions.
6. Generate the invite URl.
7. Using the url, add the bot to whichever server you want.

## Minimal Start

```py
import discord

BOT_TOKEN = 'Insert the TOKEN here'

# Set up the bot with a command prefix (e.g., "!")
intents = discord.Intents.default()
intents.message_content = True  # Enable access to message content

client = discord.Client(intents=intents)

# Event: When the bot is ready
@client.event
async def on_ready():
    print(f'Logged in as {client.user.name}')

@client.event
async def on_message(message):
    if message.author == client.user:
        return

    if message.content.startswith('$hello'):
        await message.channel.send('Hello!')

# Run the bot with your token
client.run(BOT_TOKEN)
```

Let’s name this file `example_bot.py`. Make sure not to name it `discord.py` as that’ll conflict with the library.
1. The first line just imports the library.
2. Next, we create an instance of a [`Client`](https://discordpy.readthedocs.io/en/stable/api.html#discord.Client "discord.Client"). This client is our connection to Discord.
3. We then use the [`Client.event()`](https://discordpy.readthedocs.io/en/stable/api.html#discord.Client.event "discord.Client.event") [[Nested Functions in Python#@ Symbol With Decorator|decorator]] to register an event. This library has many events. Since this library is asynchronous, we do things in a “callback” style manner.
    A callback is essentially a function that is called when something happens. In our case, the [`on_ready()`](https://discordpy.readthedocs.io/en/stable/api.html#discord.on_ready "discord.on_ready") event is called when the bot has finished logging in and setting things up and the [`on_message()`](https://discordpy.readthedocs.io/en/stable/api.html#discord.on_message "discord.on_message") event is called when the bot has received a message.
4. Since the [`on_message()`](https://discordpy.readthedocs.io/en/stable/api.html#discord.on_message "discord.on_message") event triggers for _every_ message received, we have to make sure that we ignore messages from ourselves. We do this by checking if the [`Message.author`](https://discordpy.readthedocs.io/en/stable/api.html#discord.Message.author "discord.Message.author") is the same as the [`Client.user`](https://discordpy.readthedocs.io/en/stable/api.html#discord.Client.user "discord.Client.user").
5. Afterwards, we check if the [`Message.content`](https://discordpy.readthedocs.io/en/stable/api.html#discord.Message.content "discord.Message.content") starts with `'$hello'`. If it does, then we send a message in the channel it was used in with `'Hello!'`. This is a basic way of handling commands, which can be later automated with the [discord.ext.commands – Bot commands framework](https://discordpy.readthedocs.io/en/stable/ext/commands/index.html) framework.
6. Finally, we run the bot with our login token.

## Key Concepts
#### Events
Events are triggered by actions in Discord. For example:
- `on_ready`: When the bot starts. 
- `on_message`: When a message is sent.
```py
@bot.event
async def on_message(message):
    if message.author == bot.user:  # Ignore messages from the bot itself
        return
    await message.channel.send(f"I saw your message: {message.content}")
```
#### Embeds
Embeds are rich messages with titles, descriptions, fields, and more.
Example:
```py
@bot.command()
async def info(ctx):
    embed = discord.Embed(title="Bot Info", 
	    description="This is a cool bot!", 
	    color=0x00ff00
		)
    embed.add_field(name="Author", value="Your Name", inline=False)
    embed.add_field(name="Version", value="1.0", inline=False)
    await ctx.send(embed=embed)
```

