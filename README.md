# Alpaca Roleplay Discord Bot README
A Roleplaying Discord Bot for the Alpaca & Llama Based LLMs

## Overview
Alpaca Roleplay Discordbot is a software project for running the Alpaca (or LLaMa) Large Language Model as a roleplaying discord bot. The bot is designed to run locally on a PC with as little as 8GB of VRAM. The bot listens for messages mentioning its username, replying to it's messages, or any DM's it receives, processes the message content, and generates a response based on the input.
Added support for simply DM'ing the bot for private conversations. Simply message and it will respond.

This bot differs from my other repository, Alpaca-Discord (see: https://github.com/teknium1/alpaca-discord) in a couple of ways.
The primary difference is that it offers character role playing and chat history. You can set the chat history to anything you like with !limit, but the LLAMA models can only handle 2,000 tokens of input for any given prompt, so be sure to set it low if you have a large character card.

This bot utilizes a json file some may know as a character card, to place into it's preprompt information about the character it is to role play as.
You can manually edit the json or use a tool like https://zoltanai.github.io/character-editor/ to make you a character card.
For now, we only support one character at a time, and the active character card file should be character.json

I am definitely open to Pull Requests and other contributions if anyone who likes the bot wants to collaborate on adding new features, making it more robust, etc.

Example:
![image](https://user-images.githubusercontent.com/127238744/228260843-f623d17a-fb0c-4289-ab59-eae1e676b4b7.png)


## Dependencies
You must have either the LLaMa or Alpaca model (or theoretically any other fine tuned LLaMa based model) in HuggingFace format.
Please see this github gist page on pre-requisites and other information to get and use Alpaca: https://gist.github.com/teknium1/c022705857ba943fb2b7e4470d8677fb

To run the bot, you need the following Python packages:
- `discord`
- `transformers`
- `torch`

You can install discord using pip:

`pip install discord`

Currently, Transformers module only has support for Llama through the latest github repository, and not through pip package. Install it like so:

`pip install git+https://github.com/huggingface/transformers.git`

For Pytorch you need to install it with cuda enabled. See here for commands specific to your environment: https://pytorch.org/get-started/locally/

## How the bot works
The bot uses the `discord.py` library for interacting with Discord's API and the `transformers` library for loading and using the Large Language Model.

1. It creates a Discord client with the default intents and sets the `members` intent to `True`.
2. It loads the Llama tokenizer and Llama model from the local `./alpaca/` directory.
3. It initializes a queue to manage incoming messages mentioning the bot.
4. It listens for messages and adds them to the queue if the bot is mentioned.
5. If the bot is mentioned, the roleplaying character card as well as the last N messages (that you set) are sent above your prompt to the model.
6. It then processes the queue to generate responses based on the text.
7. It sends the generated response to the channel where the original message was sent. 

## How to run the bot
1. Ensure you have the required dependencies installed.
2. Create a Discord bot account and obtain its API key. Save the key to a file named `alpacakey.txt` in the same directory as the bot's script.
3. Make sure the Llama tokenizer and Llama model are stored in a local `./alpaca/` directory - They should be HuggingFace format.
Your alpaca directory should have all of these files (example image is from alpaca-7b - 13B+ models will have more files):  
![image](https://user-images.githubusercontent.com/127238744/226094774-a5371a98-947b-47a4-a4b2-f56e6331ee1e.png)  
4. Run the script using Python:
`python roleplay-bot.py`
5. Invite the bot to your Discord server by generating a URL in the discord developer portal.
6. Mention the bot in a message or dm the bot directly to receive a response generated by the Large Language Model.

## Customization options
You can customize the following parameters in the script to change the behavior of the bot:

- `load_in_8bit`: Set to `True` if you want to load the model using 8-bit precision.
- `device_map`: Set to `"auto"` to automatically use the best available device (GPU or CPU).
- `max_new_tokens`: Set the maximum number of new tokens the model should generate in its response.
- `do_sample`: Set to `True` to use sampling instead of greedy decoding for generating the response.
- `repetition_penalty`: Set a penalty value for repeating tokens. Default is `1.0`.
- `temperature`: Set the sampling temperature. Default is `0.8`.
- `top_p`: Set the cumulative probability threshold for nucleus sampling. Default is `0.75`.
- `top_k`: Set the number of tokens to consider for top-k sampling. Default is `40`.
- `message_history_limit`: set this to the default number of previous chat messages for the bot to look at each response it makes

## Credits, License, Etc.
While my repo may be licensed as MIT, the underlying code, libraries, and other portions of this repo may not be. Please DYOR to check what can
and can't be used and in what ways it may or may not be. If anyone can help me with proper attributions or licensing placement, please submit a PR

This would not be possible without the people of Facebook's Research Team: FAIR, and with Stanford's Research:
<pre>
@misc{alpaca,
  author = {Rohan Taori and Ishaan Gulrajani and Tianyi Zhang and Yann Dubois and Xuechen Li and Carlos Guestrin and Percy Liang and Tatsunori B. Hashimoto },
  title = {Stanford Alpaca: An Instruction-following LLaMA model},
  year = {2023},
  publisher = {GitHub},
  journal = {GitHub repository},
  howpublished = {\url{https://github.com/tatsu-lab/stanford_alpaca}},
}
</pre>

@Ristellise - https://github.com/Ristellise - For converting the code to be fully async and non-blocking

@Main - https://twitter.com/main_horse - for helping with getting the initial inferencing code working

You can find me on Twitter - @Teknium1 - https://twitter.com/Teknium1

Final thanks go to GPT-4, for doing much of the heavy lifting for creating both the original discord bot code, and writing a large portion of this readme! 
