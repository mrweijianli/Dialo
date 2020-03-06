# Dialo

<!-- ```
User >>> Hello
Bot >>> Hello, nice to meet you!
User >>> Where are you from?
Bot >>> I'm from England, but I live in the US, USA
User >>> Which state are you in?
Bot >>> Alabama, my friend
User >>> What's the weather there?
Bot >>> It's cloudy
``` -->

<!-- Dialo implements 
  - a decoder ([source]()) for [DialoGPT](https://github.com/microsoft/DialoGPT), 
  - an interactive multiturn chatbot ([source]()), and 
  - a Telegram chatbot ([source]()).
  
The bot is built around [DialoGPT](https://github.com/microsoft/DialoGPT) - a large-scale pretrained dialogue response generation model trained by Microsoft, which was trained on 147M multi-turn dialogue from Reddit discussion thread. The human evaluation results indicate that its quility is comparable to human response quality under a single-turn conversation Turing test.

Since even with properly filtered Reddit dataset the model can generate toxic/inappropriate responses, the Microsoft team was unable to provide the decoding script. This repository implements the decoding script inspired by `run_generation.py` released earlier by Hugging Face. Moreover, it implements a Telegram bot that can be deployed locally, remotely, and even on Colab, and just makes testing fun. -->

## Problem we tried to solve
In this project, we intended to develop a contextual chit-chat chatbot that has a user-friendly user interface and is easy to be deployed on any cloud platform.

## Core Model
This robot is developed based on the model, [DialoGPT](https://github.com/microsoft/DialoGPT), which is based on the language model, [GPT2](https://openai.com/blog/better-language-models/).

## How to run the final deliverable (2 options)
## Containerized way:
### 1. Create a Telegram bot
Please follow this [link](https://tutorials.botsfloor.com/creating-a-bot-using-the-telegram-bot-api-5d3caed3266d) to create a Telegram bot. Please write down the token from the response of Telegram for later use.
```
Use this token to access the HTTP API:
2764xxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxx
```
### 2. Clone this repo and enter the repo
```
git clone https://github.com/Leevisir/Dialo.git
cd Dialo
```
### 3. Put the API token into the configuration file
```
# change this line in the file gpt2bot/chatbot.cfg
telegram_token = <YOUR_TOKEN_HERE>
```
### 4. Build the Docker imgae and run it
```
docker build -t dialo .
docker run dialo
```
Now the chatbot is running and you can use Telegram 

### 3. Create a virtual environment and activate it (if anaconda is not installed, please install it first following this [link](https://docs.anaconda.com/anaconda/install/))
```
conda create -n dialo python=3.7
conda activate dialo
```
### 4. Install all requirements
```
pip install -r requirements.txt
```
### 5. 
  
## What we did?

### 1. Create a Telegram bot

- Register a new Telegram bot via BotFather (see https://core.telegram.org/bots)

### 2. Deploy the bot (4 options)

#### a. Google Colab

[A Colab interactive notebook](https://colab.research.google.com/drive/1QH9Vq6EEl7lU6Nz7uFHFN5i6rogLaAE2)

A good thing about Google Colab is free GPU. So why not running the Telegram bot there, for blazingly fast chat? Run the notebook at daytime and do not forget to stop it at night.

#### b. Amazon EC2
<!-- First, search for EC2 in the AWS console search bar:
![image info](./figures/EC2_search.png)
On the EC2 Dashboard, launch a new EC2 instance:
![image info](./figures/launch_instance.png) -->
First, launch a new EC2 instance
Select the correct AMI:
![iamge info](./figures/ubuntu_instance.png)
Then, select the correct Instance Type with GPU supports. Then one we chose was **p3.2xlarge**  
After launching the EC2 instance, on the sidebar of the EC2 Dashboard, click **instance**:
![image info](./figures/ec2_sidebar.png)



#### c. Amazon ECS

#### d. Local laptop

- Clone the repository
- Set your parameters such as API token in dialog.cfg
- To avoid re-downloading model files at each re-deployment, download the model files beforehand with
```
# cd gpt2bot/gpt2bot
python model.py
```
- Finally, deploy the container from the root folder
```
docker build -t gpt2bot . && docker run gpt2bot
```

#### Manually

- Clone the repository
- Set your parameters such as API token in dialog.cfg
- Install packages listed in requirements.txt
- Run the script
```
# cd gpt2bot/gpt2bot
python telegram_bot.py
```
- To test the things out in the console, run
```
python interactive_bot.py
```

### 3. Start chatting!

![](telegram_bot.gif)

Just start texting. Append @gif for the bot to generate a GIF instead of text. To reset, type "Bye".


## References

- [Official DialoGPT implementation](https://github.com/microsoft/DialoGPT) and [DialoGPT paper](https://arxiv.org/abs/1911.00536)
- [Thread on current decoding scripts](https://github.com/microsoft/DialoGPT/issues/3)

You can wait for a full DialoGPT release and then replace the decoder.
