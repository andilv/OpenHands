# Understanding OpenHands and its LLM Configuration

## What is an LLM?

LLM stands for **Large Language Model**. In simple terms, think of an LLM as a very advanced AI that has been trained on a massive amount of text and code. This training allows it to understand and generate human-like text, translate languages, write different kinds of creative content, and answer your questions in an informative way. It's like having a super-smart assistant that's very good with words and information.

## OpenHands and LiteLLM

**OpenHands** is a project that aims to replicate the functionality of OpenAI's "Hands" project, likely referring to a system that can understand and execute tasks based on natural language instructions. To interact with these powerful LLMs, OpenHands uses a clever tool called **LiteLLM**.

## LiteLLM: The Universal Translator for LLMs

Think of **LiteLLM** as a universal adapter or translator. Different companies and research groups create various LLMs (like those from OpenAI, Anthropic, Cohere, or open-source models). Each ofthese LLMs might have its own way of receiving requests and sending back responses.

LiteLLM simplifies this by providing a single, consistent way for OpenHands to talk to many different LLMs. So, instead of OpenHands needing to learn how to communicate with each LLM provider individually, it just talks to LiteLLM, and LiteLLM handles the specific communication details for the chosen LLM provider.

This is incredibly useful because it gives OpenHands flexibility. You're not locked into using just one LLM provider.

## Connecting to Various LLM Providers

Because OpenHands uses LiteLLM, it can connect to a wide array of LLM providers. This includes:

*   **OpenAI:** This is one of the most well-known LLM providers, offering models like GPT-3.5, GPT-4, etc.
*   **Azure OpenAI:** Microsoft's Azure platform also provides access to OpenAI models.
*   **Anthropic:** Another company developing powerful LLMs (e.g., Claude).
*   **Cohere:** Offers LLMs focused on enterprise use cases.
*   **Many others:** LiteLLM supports a long list of other proprietary and open-source LLM providers.

## What is an "OpenAI-Compatible Endpoint"?

An "OpenAI-compatible endpoint" refers to a service or a self-hosted LLM that mimics the way OpenAI's API (Application Programming Interface) works.

Imagine OpenAI has a specific set of rules and formats for how you send requests to their LLMs and how you receive responses. An "OpenAI-compatible endpoint" follows these same rules and formats, even if the underlying LLM isn't actually an OpenAI model.

**Why is this important?**

*   **Ease of Use:** If a tool (like OpenHands, via LiteLLM) is already set up to talk to OpenAI's API, it can easily talk to any OpenAI-compatible endpoint without needing significant changes. The tool sends the request in the "OpenAI format," and the compatible endpoint understands it and responds in the same format.
*   **Flexibility with Self-Hosted or Different Models:** This allows developers to use open-source LLMs (like Llama, Mixtral, etc.) or other commercial models that have chosen to offer an OpenAI-compatible interface. You might run these models on your own servers or use a smaller, specialized LLM that is more cost-effective for certain tasks, all while using the same integration logic you'd use for OpenAI.

In essence, OpenHands, through LiteLLM, can easily connect to official OpenAI models or other LLMs that have adopted the OpenAI API structure, providing a broad range of choices for users.
