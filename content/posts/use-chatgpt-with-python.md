+++
title = "Your Simple Guide to use ChatGPT via the OpenAI API"
description = ""
tags = [
    "artificial intelligence",
    "chatgpt",
    "python",
]
date = "2024-03-01"
categories = [
    "article",
]
menu = "main"
+++



ChatGPT is a state-of-the-art language model developed by [OpenAI](https://openai.com/). It serves many purposes in natural language processing, including language translation, chatbots, and story writing, among others.

This guide describes how to utilize ChatGPT through the OpenAI API service on macOS operating systems. Additionally, it provides instructions for interacting with ChatGPT using Python.

---
## Connect to ChatGPT via API
To set up ChatGPT API follow these instructions:

1. Set up an API Key
Sign up to [OpenAI](https://beta.openai.com/signup/) and follow the indications to [create a new secret key](https://beta.openai.com/signup/). All your API requests must include this API Key in the Authorization HTTP header of the request.

{{< hint danger >}}
**Important:**  
Keep in a safe location your new secret key. For security reasons, you won’t be able to retrieve it again; thus, you’ll need to generate a new one.
{{< /hint >}}

2. Open terminal
3. Start making some requests using the OpenAI API client and your API Key. For further information, refer to [Making Requests](https://platform.openai.com/docs/api-reference/making-requests).

    To request all available models, use the following request:

    ```python
    curl https://api.openai.com/v1/models \
    -H "Authorization: Bearer <YOUR_API_KEY>"
    ````

    To retrieve information about the `text-davinci-003` model, use the following request:

    ```python
    curl https://api.openai.com/v1/models/text-davinci-003 \
    -H "Authorization: Bearer <YOUR_API_KEY>"
    ```

    To make a completion, use the following request:

    ```python
    curl https://api.openai.com/v1/completions \   
    -H "Content-Type: application/json" \   
    -H "Authorization: Bearer <YOUR_API_KEY>" \   
    -d '{
        "model": "text-davinci-003",
       "prompt": "Say this is a test",
       "max_tokens": 7,
       "temperature": 0
     }'
    ```

---
## Use ChatGPT with Python 
This section describes how to set up ChatGPT and use it in your Python scripts.

### Prerequisites
Ensure you comply with the following requirements before you continue:

- [Set up an API Key](https://platform.openai.com/account/api-keys)
- Install [Python](https://www.python.org/downloads/) version 2.7 or later
To check your current Python version, type the following command in the terminal `python3-version`

### Set up ChatGPT with Python
To integrate ChatGPT with your Python scripts:

1. Open terminal
2. Create a new empty project folder:

    ```python
    mkdir chatgpt-python
    cd chatgpt-python
    ```

3. Install the OpenAI Python library:

    ```python
    pip3 install openai
    ```

4. Create a new file chat.pyin the project folder and edit its content:

    ```python
    touch chat.py 
    nano chat.py
    ```

5. Create a completion request sample using the following template:

    ```python
    import openai

    # Set up OpenAI API client
    openai.api_key = "<YOUR_API_KEY>"

    # Set up OpenAI model and prompt
    model = "text-davinci-003"
    prompt = "Hello, how are you today?"

    # Generate a request
    completion = openai.Completion.create(
        engine=model,
        prompt=prompt,
        max_tokens=1024,
        n=1,
        stop=None,
        temperature=0,
    )

    response = completion.choices[0].text
    print(response)
    ```

6. Save the chat.pyfile.

7. Make the completion request by running the chat.pyscript.

    ```python
    python3 chat.py
    ```

    You get the following sample response:

    ```python
    I am doing well, thank you. How about you?
    ```

    Refer to [Making Requests](https://platform.openai.com/docs/api-reference/making-requests) for additional information.

---

Trusting this comes in handy for you!