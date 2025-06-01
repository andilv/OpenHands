# Step-by-Step Guide: Configuring a Custom OpenAI-Compatible Endpoint in OpenHands UI

This guide will walk you through configuring OpenHands to use your custom OpenAI-compatible LLM endpoint via the OpenHands user interface (UI).

**Before You Start:** Make sure you have the following information ready (as detailed in the "Prerequisites" guide):
*   Your custom OpenAI-compatible endpoint URL.
*   Your API key for this endpoint (if applicable).
*   The exact model name served by your endpoint.

Let's begin:

1.  **Navigate to Settings:**
    *   Open the OpenHands application.
    *   On the main screen or sidebar, look for a **Settings** menu item or an icon (often shaped like a gear ⚙️). Click on it to open the settings panel.

2.  **Locate LLM/Model Configuration:**
    *   Within the Settings panel, find the section related to **LLM Configuration**, **Model Settings**, or **Agent Settings**. The exact naming might vary.
    *   This is where you'll tell OpenHands which language model to use.

3.  **Enable Advanced Options (If Necessary):**
    *   Some UIs hide more detailed settings under an "Advanced," "Advanced Options," or "Custom Settings" toggle or button. If you see such an option, enable it to reveal the fields needed for a custom endpoint.

4.  **Configure the LLM Settings:**
    You will typically see a few key fields to fill in. Here's how to approach them for your custom OpenAI-compatible endpoint:

    *   **LLM Provider** (or similar field):
        *   **If "OpenAI" is an option:** You can often select **"OpenAI"** from the dropdown list. Even though you're using a custom endpoint, selecting "OpenAI" tells LiteLLM (the underlying library OpenHands uses) to format requests according to the OpenAI API specification. The **Base URL** you provide later will redirect these requests to your custom endpoint.
        *   **If there's no "OpenAI" option or it's unclear:** Don't worry. The crucial part is correctly setting the "Base URL" and "Model" fields. LiteLLM is designed to infer the provider type based on these.

    *   **Model** (or **Custom Model**, **Model Name**):
        *   **Format:** Enter your model name using the format `openai/<your-model-name>`.
        *   **`<your-model-name>`:** Replace this with the exact model name you identified in the prerequisites. This could be something like `gpt-3.5-turbo`, `MyCustomGPT4`, `mistralai/Mistral-7B-Instruct-v0.1`, or `llama2-chat`.
        *   **Why `openai/` prefix?** This prefix is a common convention used by LiteLLM to explicitly indicate that the model, even if custom-named or hosted elsewhere, expects to communicate using the OpenAI API structure. It helps LiteLLM correctly route and format the requests.
        *   **Examples:**
            *   `openai/gpt-4o`
            *   `openai/MyCustomLlama3`
            *   `openai/mistralai/Mistral-7B-Instruct-v0.1` (if your endpoint serves this specific Hugging Face model name)
            *   `openai/ollama/llama2` (some LiteLLM configurations might use this for Ollama, but often just `openai/llama2` with the correct Base URL is sufficient)

    *   **API Base URL** (or **Base URL**, **Endpoint URL**, **Server URL**):
        *   Enter your **full custom OpenAI-compatible endpoint URL** here.
        *   **Crucial:** Ensure it includes `http://` or `https://` at the beginning.
        *   This URL tells LiteLLM *where* to send the API requests, overriding the default OpenAI servers.
        *   **Examples:**
            *   `http://localhost:11434/v1` (Common for local Ollama, note the `/v1` which is standard for OpenAI compatibility)
            *   `https://api.yourcustomprovider.com/v1`
            *   `http://your-internal-ip:8000/v1/chat/completions` (The exact path like `/v1/chat/completions` or just `/v1` depends on your endpoint's specific setup. Always check its documentation.)

    *   **API Key:**
        *   Enter the **API key** for your custom endpoint.
        *   **If your custom endpoint does not require an API key:**
            *   Try using a placeholder value like `NA`, `none`, `ollama`, `placeholder`, or `dummy`.
            *   Sometimes, leaving the field blank is also acceptable.
            *   **Always consult the documentation for your specific custom endpoint or the tool serving it (like Ollama or vLLM) to know the correct placeholder or if it can be omitted.** Using an incorrect placeholder for an endpoint that *does* expect a key (or vice-versa) will lead to connection errors.

5.  **Save Your Configuration:**
    *   Look for a **Save**, **Apply**, or **Update Settings** button. Click it to save your new LLM configuration.

6.  **Test the Configuration:**
    *   If there's a "Test Connection" button, use it.
    *   Otherwise, try running a simple task in OpenHands that would require LLM interaction to see if it works. Check for any error messages.

**Important Tips:**

*   **Typos:** Double-check every field for typos, especially the Base URL and Model name. These need to be exact.
*   **URL Scheme:** Ensure your Base URL starts with `http://` (for unencrypted local connections) or `https://` (for secure connections).
*   **Leading/Trailing Spaces:** Make sure there are no accidental spaces at the beginning or end of your inputs, especially for the API key and URL.
*   **Endpoint Documentation:** Your custom endpoint's documentation is your best friend! It will have the definitive information on the correct Base URL, expected model names, and API key requirements.
*   **OpenHands Logs:** If you encounter issues, check the OpenHands application logs. They often provide detailed error messages that can help you troubleshoot connection problems with LiteLLM and your custom endpoint.

By following these steps, you should be able to successfully configure OpenHands to work with your preferred OpenAI-compatible LLM endpoint.
