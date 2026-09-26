# Discord-BobTheBot
My Discord Bot Bob
heres my BobTheBot code :D 
import discord
import random
from discord.ext import commands
from DiscordBobTheBotLogic import gen_pass, gen_emoji, flip_coin
print("bot.py started")

intents = discord.Intents.default()
intents.message_content = True

bot = commands.Bot(command_prefix="Hey Bob ", intents=intents)

@bot.event
async def on_ready():
    print(f"Bob The Bot is ready! {bot.user.name}")

@bot.command()
async def hello(ctx):
    await ctx.send(f"Hello! I'm Bob The Bot! {ctx.author.mention}")

@bot.command()
async def emoji(ctx):
    await ctx.send(gen_emoji())

@bot.command()
async def coin(ctx):
    await ctx.send(f"The coin landed on: {flip_coin()}")

@bot.command()
async def password(ctx, length: int = 10):
    await ctx.send(f"Your password is: `{gen_pass(length)}`")
    elements = "+-/*!&$#?=@abcdefghijklnopqrstuvwxyzABCDEFGHIJKLMNOPQRSTUVWXYZ1234567890"
    password = ""
    for _ in range(password):
      password += random.choice(elements)
      return password
    
def gen_pass(pass_length):
    elements = "+-/*!&$#?=@abcdefghijklnopqrstuvwxyzABCDEFGHIJKLMNOPQRSTUVWXYZ1234567890"
    password = ""
    for _ in range(pass_length):
        password += random.choice(elements)
    return password    

print("bot.py started")
token = discord.getenv("My_Super_Secret_Bob_Token")
if token:
    print("Token found, starting bot...")
    bot.run(token)
else:
    print("DISCORD_TOKEN was not found.")
