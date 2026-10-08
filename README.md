# Discord-BobTheBot
# English/inglés ↓
# My Discord Bot Bob heres my BobTheBot code :D 
# You can use this code for your bot and add more thing to yours o(^▽^)o
# Español/Spanish ↓
# Mi bot de Discord Bob aquí está el código de BobTheBot :D
# Puedes usar este código para tu bot y añadirle más cosas o(^▽^)o

import os
import requests
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
    await ctx.send(f"Hello! I'm Bob The Bot! :D {ctx.author.mention}")

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
    
async def gen_pass(pass_length):
    elements = "+-/*!&$#?=@abcdefghijklnopqrstuvwxyzABCDEFGHIJKLMNOPQRSTUVWXYZ1234567890"
    password = ""
    for _ in range(pass_length):
        password += random.choice(elements)
    return password    

@bot.command()
async def images(ctx):
    images = os.listdir("image")
    images_send = random.choice(images)
    
    with open(f"image/{images_send}", "rb")as f:
        picture = discord.File(f)
    await ctx.send(file=picture)

def get_duck_image_url():    
    url = 'https://random-d.uk/api/random'
    res = requests.get(url)
    data = res.json()
    return data['url']


@bot.command('duck')
async def duck(ctx):
    '''Una vez que llamamos al comando duck, 
    el programa llama a la función get_duck_image_url'''
    image_url = get_duck_image_url()
    await ctx.send(image_url)
    
print("bot.py started")

bot.run("Your_Bot_Token_Goes_Here!")
