---
title: OpenAI - New Announcements at DevDay
date: 2023-11-28
categories:
---
# Summary

1. **GPT-4 Turbo**: A new, more capable model with a 128K context window and knowledge of world events up to April 2023, offered at lower prices.
2. **Function Calling Updates**: Enhanced ability to output JSON objects for function calls, improving accuracy and multi-function handling in a single message.
3. **Improved Instruction Following and JSON Mode**: Enhanced performance in following specific instructions and support for JSON mode in the API.
4. **Reproducible Outputs and Log Probabilities**: New `seed` parameter for consistent outputs, useful for debugging and testing, and upcoming features for log probabilities.
5. **Updated GPT-3.5 Turbo**: A new version supporting a 16K context window, improved instruction following, JSON mode, and parallel function calling.
6. **Assistants API, Retrieval, and Code Interpreter**: A new API for building AI assistants with capabilities like Code Interpreter and Retrieval, offering persistent threads and function calling.
7. **GPT-4 Turbo with Vision**: Ability to accept images as inputs in the Chat Completions API for various use cases like caption generation and image analysis.
8. **DALL·E 3 Integration**: Availability for developers to integrate DALL·E 3 into their applications for image generation and design.
9. **Text-to-Speech (TTS) API**: A new API for generating human-quality speech from text, with multiple voice options and two model variants.
10. **GPT-4 Fine Tuning and Custom Models**: Experimental access to GPT-4 fine-tuning and a program for training custom GPT-4 models for organizations with large proprietary datasets.
11. **Lower Prices and Higher Rate Limits**: Reduced prices for various models and doubled tokens per minute limit for GPT-4 customers.
12. **Copyright Shield**: A new feature to protect customers from legal claims around copyright infringement.
13. **Whisper v3 and Consistency Decoder**: Release of Whisper large-v3 for improved automatic speech recognition and the open-sourced Consistency Decoder for image improvement.

# Details

## Function calling
Function calling in ChatGPT allows the model to interact with external applications or APIs by generating a JSON object with the necessary parameters to execute a function. For example, if you have an app that controls smart home devices, you could describe functions like `turnOnLight` or `adjustThermostat` to the model. When prompted, ChatGPT can generate a JSON object with the correct parameters, like `{ "function": "turnOnLight", "parameters": { "room": "living room" } }`.

The recent update to function calling has made it more versatile. Now, it's possible to call multiple functions in a single message. For instance, if a user sends a message saying “open the car window and turn off the A/C”, the model can intelligently generate a JSON object containing arguments for both functions, where previously this would have required multiple interactions with the model.

### Using Chat Completions API

The basic sequence of steps for function calling is as follows:

1. Call the model with the user query and a set of functions defined in the [functions parameter](https://platform.openai.com/docs/api-reference/chat/create#chat/create-functions).
2. The model can choose to call one or more functions; if so, the content will be a stringified JSON object adhering to your custom schema (note: the model may hallucinate parameters).
3. Parse the string into JSON in your code, and call your function with the provided arguments if they exist.
4. Call the model again by appending the function response as a new message, and let the model summarize the results back to the user.

### Using Assistants Tools Page

## Improved Instruction Following and JSON Mode

The Improved Instruction Following and JSON Mode release for ChatGPT, particularly in the GPT-4 Turbo model, refers to two key enhancements:

1. **Improved Instruction Following**: This improvement means the model performs better at tasks that require careful adherence to specific instructions. For instance, if you ask the model to generate responses in a particular format like XML or JSON, it's now more capable of doing so accurately.

2. **JSON Mode**: This is a new feature in the API where the model can be instructed to respond with valid JSON. The addition of a `response_format` parameter in the API ensures that the model's output is constrained to syntactically correct JSON. This is particularly useful for developers who need to generate JSON responses for their applications outside of the function calling context.

## Reproducible Outputs and Log Probabilities

## Assistants API, Retrieval, and Code Interpreter

The [Assistants API](https://platform.openai.com/docs/guides/assistants) enables developers to easily build powerful AI assistants within their apps. This API removes the need to manage conversation history and adds access to OpenAI-hosted tools like Code Interpreter and Retrieval. The API also supports improved function-calling for 3rd party tools.

An Assistant represents a purpose-built AI that uses OpenAI’s [models](https://platform.openai.com/docs/models), access files, maintain persistent threads and call tools.

A thread is a conversation session between an assistant and a user. Threads simplify application development by storing message history and truncating it when the conversation gets too long for the model’s context length.

Code Interpreter is priced at $0.03 / session. If your assistant calls Code Interpreter simultaneously in two _different_ _threads_, this would create two Code Interpreter sessions (2 * $0.03). Each session is active by default for one hour, which means that you would only pay this fee once if your user keeps giving instructions to Code Interpreter in the same thread for up to one hour.

Retrieval is priced at $0.20/GB per assistant per day. If your application stores 1GB of files for one day and passes it to two Assistants for the purpose of retrieval (e.g., customer-facing Assistant #1 and internal employee Assistant #2), you’ll be charged twice for this storage fee (2 * $0.20 per day). This fee does not vary with the number of end users and threads retrieving knowledge from a given assistant.

Code Interpreter allows the Assistants API to write and run Python code in a sandboxed execution environment. This tool can process files with diverse data and formatting, and generate files with data and images of graphs. Code Interpreter allows your Assistant to run code iteratively to solve challenging code and math problems. When your Assistant writes code that fails to run, it can iterate on this code by attempting to run different code until the code execution succeeds.

Code Interpreter is charged at $0.03 per session. If your Assistant calls Code Interpreter simultaneously in two different threads (e.g., one thread per end-user), two Code Interpreter sessions are created. Each session is active by default for one hour, which means that you only pay for one session per if users interact with Code Interpreter in the same thread for up to one hour.
## GPT-4 Turbo with Vision
GPT-4 with vision is currently available to all [developers who have access to GPT-4](https://help.openai.com/en/articles/7102672-how-can-i-access-gpt-4) via the `gpt-4-vision-preview` model and the Chat Completions API which has been updated to support image inputs. Note that the [Assistants API](https://platform.openai.com/docs/api-reference/assistants) does not currently support image inputs.
## DALL·E 3 Integration

## Text-to-Speech (TTS) API

## GPT-4 Fine Tuning and Custom Models
By default OpenAI’s models are trained to be helpful generalist assistants. Fine-tuning can be used to make a model which is narrowly focused, and exhibits specific ingrained behavior patterns. Retrieval strategies can be used to make new information available to a model by providing it with relevant context before generating its response. Retrieval strategies are not an alternative to fine-tuning and can in fact be complementary to it.

GPT-4 fine-tuning is in experimental access and eligible developers can request access via the [fine-tuning UI](https://platform.openai.com/finetune). Currently, `gpt-3.5-turbo-1106` supports up to 16K context examples

## Copyright Shield

We will now step in and defend our customers, and pay the costs incurred, if you face legal claims around copyright infringement. This applies to generally available features of ChatGPT Enterprise and our developer platform.

## Whisper v3 and Consistency Decoder

## Others interesting notebooks


# References
- [New models and developer products announced at DevDay](https://openai.com/blog/new-models-and-developer-products-announced-at-devday)
- [OpenAI DevDay, Opening Keynote](https://www.youtube.com/watch?v=U9mJuUkhUzk&t=2290s)
- [OpenAI Community Forum](https://community.openai.com/)
- [OpenAI Function Calling](https://platform.openai.com/docs/guides/function-calling)
- [Assistants API](https://help.openai.com/en/articles/8550641-assistants-api)
- [Assistan's Playground](https://platform.openai.com/playground)


