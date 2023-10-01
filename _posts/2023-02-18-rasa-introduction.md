---
layout: post
title: Introduction to Rasa - A framework for building chatbots
read: 8
post-image: /assets/images/posts/10_rasa_intro/post.jpg
description: Rasa - A Python framework for building conversational AI chatbots using Natural Language Understanding (NLU)
categories: software development
---

---

![](/assets/images/posts/10_rasa_intro/post.jpg)

With the towering capabilities of ChatGPT, chatbots have been the talk of the town for a while now. Many companies are offering conversational chatbots for users as a tool to improve customer service and to reduce the workload of customer support teams. These conversational chatbots are superior to rule-based chatbots with their ability to mimic the way humans converse, rather than forcing users to ask specific questions using specific phrases and replying with fixed answers.

With new tools, frameworks and libraries, building a chatbot yourself has never been easier. Many frameworks for building chatbots are open-source, such as <a href="https://rasa.com/" target="_blank">Rasa</a>, <a href="https://dev.botframework.com/">Microsoft Bot Framework</a>, <a href="https://dev.botframework.com/">LangChain</a>, etc., which allows you to build a chatbot at practically no cost.

This post explains how Rasa works, particularly how a Rasa chatbot replies to a user query, and to how to set up Rasa and get started.

- [Rasa - A Python framework](#rasa---a-python-framework)
- [How does Rasa work?](#how-does-rasa-work)
- [From Query to Reply](#from-query-to-reply)
- [Setting up Rasa](#setting-up-rasa)

# Rasa - A Python framework
**Rasa** is an open-source <a href="https://github.com/RasaHQ/rasa" target="_blank">**Python** framework</a> for building chatbots using **Natural Language Understanding (NLU)**.

<hr style="border-style: dashed">

### Natural Language Understanding (NLU)
There are 2 key terms related to NLU: **intents** and **entities**.
- **Intents**: Intentions of the user's query.
- **Entities**: Keywords that provide specific data that needed to be extracted from the query.

For example: Where can I find a Chinese restaurant?
- Intent: find a restaurant
- Entity: cuisine - Chinese

<hr style="border-style: dashed">

With NLU, the chatbot can understand and classify users' intentions based on their queries, and extract useful information from the queries. The Rasa SDK comes with its own NLU model (the <a href="https://rasa.com/blog/introducing-dual-intent-and-entity-transformer-diet-state-of-the-art-performance-on-a-lightweight-architecture/" target="_blank">**DIET classifier**</a>) that can be trained with your own data for intent classification and entity extraction. 

Apart from NLU support, the SDK also comes with chatbot conversation handlers:
- a **tracker store** to store conversation history
- a **lock store** to ensure that incoming messages for a conversation are processed in the right order. 

It also provides **API endpoints** for integration with other systems, a <a href="https://chat-widget-docs.rasa.com/?path=/docs/rasa-chat-widget--widget" target="_blank">**chat widget**</a> to display on your own website, and **connectors** to various channels such as Messenger, Slack, Telegram, etc.

# How does Rasa work?

There are 2 major steps for how a chatbot works:
1. Understand the intention and extract information from the user's query.
2. Determine the action and the reply to the query based on the intention and information.

## First Step {#firststep}
In Rasa, the first step is achieved with its NLU model. While the DIET classifier performs both intent classification and entity extraction, Rasa allows you to customise the <a href="https://rasa.com/docs/rasa/components#intent-classifiers" target="_blank">**intent classification**</a> and <a href="https://rasa.com/docs/rasa/components#entity-extractors" target="_blank">**entity extraction**</a> processes independently using other models. 

A set of **intents** are predefined during the training of the bot, for eg. "greet", "find_restaurant", "place_order", etc. Same goes to the **entities**, for eg. "cuisine", "food", "amount".

In the first step,
- the user query is classified with an intent (or a combination of intents)
- entities are extracted.

```
Where can I find a Chinese restaurant?
> Intent: find_restaurant
> Entities: {cuisine: "chinese"}
```

## Second Step {#secondstep}
In the second step, a separate model will predict an **action** that the chatbot should perform next based on the intents and entities obtained from the first step. The action includes any backend processes to be performed and the reply to the user. The backend processes may be searching the database for restaurants, placing an order, etc.

To allow us to train the model, Rasa uses **Stories** and **Rules**. Both stories and rules are methods for us to map out potential conversation paths. The model will then learn from these paths during training to generalise to unseen paths when in use.

### Story
A **story** is a representation of a conversation between a user and the bot. The user query is represented with the intent classfied, and the bot's reply is represented with an Action.

{% highlight yaml %}
- story: search restaurant          # name of the story
  steps:
  - intent: greet                   # "Hello"
  - action: utter_ask_howcanhelp    # "How can I help?"
  - intent: find_restaurant         # "Where can I find a Chinese restaurant?"
    entities:
    - cuisine: "chinese"
  - action: utter_processing        # "Alright. Give me a second."
  - action: action_find_restaurant  # Search database for restaurant, 
                                    # "The nearest Chinese restaurant is in ..."
{% endhighlight %}

### Rule

A rule is similar to a story, only that it usually is reserved for short pieces of conversations that should always follow the same path.

{% highlight yaml %}
- rule: always say bye when user says bye       # name of the rule
  steps:
  - intent: bye                     # "Goodbye"
  - action: utter_bye               # "Goodbye, hear from you soon"
{% endhighlight %}

A rule will take precedence over a story when deciding the action.

# From Query to Reply

Diving deeper for the full picture:

<figure>
<img src="/assets/images/posts/10_rasa_intro/query_to_reply.jpg" alt="From query to reply">
<figcaption>The process of converting query to reply</figcaption>
</figure>

When user inputs a query, the text is first converted into **tokens** (process a) using a **tokeniser**. A tokeniser splits text into tokens - words, characters or some subwords.

In process b, the tokens are converted into **features** using a **featuriser**. Two types of features are created: **sequence features** and **sentence features**. Each sequence feature represents each token, while the sentence feature is a feature over all tokens - the query sentence itself. For "Where can I find a Chinese restaurant?", splitting it into word tokens (7 tokens in total), there will be 7 sequence features and 1 sentence feature.

Process c is the NLU step descibed [here](#firststep), while processes d and e are the action-prediction steps described [here](#secondstep).

# Setting up Rasa

Prerequisite: Python 3.7 to 3.10 (as of February 2023)

## Python virtual environment

Once python is installed, create a virtual environment for your project. Go to the directory where you will setup your project and run the following command in your command prompt or terminal to create a virtual environment named `venv`:

    python3 -m venv ./venv

Activate the virtual environment once created:
- cmd (Windows)

        .\venv\Scripts\activate

- terminal (macOS, Linux)

        source ./venv/bin/activate

You should see the name of the environment in your cmd/terminal in brackets.

    (venv) ...

Check that the python version is correct by doing so:

    python --version

**!! Remember to activate your virtual environment every time you work on the project.**

## rasa

Install rasa with the following command:

    pip install rasa

Once installed, check if everything is installed correctly:

    rasa --version

You can now create a new project with:

    rasa init

Detailed instructions of the setup can also be found in <a href="https://rasa.com/docs/rasa/installation/environment-set-up" target="_blank">Rasa's official documentation</a>.

# Conclusion
- **Rasa** is an open-source **Python** framework for building chatbots using **Natural Language Understanding (NLU)**.
- There are 2 major steps:
    - Understanding intent and extract entities from user's query.
    - Plan and decide the next action and what to reply.
- Rasa achieves both steps with its built-in DIET classifier model, and stories and rules.

---

**Author**: <a href="https://github.com/andreusjh99" target="_blank">Chia Jing Heng (andreusjh99)</a>