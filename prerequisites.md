# Prerequisites for Using a Custom OpenAI-Compatible Endpoint with OpenHands

To configure OpenHands to use your own custom Large Language Model (LLM) setup, you'll need a few key pieces of information. This setup relies on your custom LLM service exposing an "OpenAI-compatible endpoint," meaning it communicates in the same way that OpenAI's official services do.

Here are the essential prerequisites:

### 1. An Accessible Custom OpenAI-Compatible Endpoint URL

*   **What it is:** This is the web address (Uniform Resource Locator) where your custom LLM service can be reached. It's like the street address for your LLM. OpenHands will send its requests (e.g., "summarize this text") to this URL.
*   **Why it's needed:** Without this URL, OpenHands has no way to find and communicate with your custom LLM. It's the fundamental connection point.
*   **Where to find it:**
    *   **Cloud LLM Providers (not OpenAI directly):** If you're using a managed LLM service from a provider that offers OpenAI-compatible endpoints (e.g., Azure OpenAI, or other smaller providers), this URL will be provided in their dashboard, documentation, or during the setup process of your deployed model.
    *   **Self-Hosted LLMs:** If you or your organization has set up an open-source LLM (like Llama, Mixtral, etc.) using tools like vLLM, Ollama (with an OpenAI-compatible interface), or a custom FastAPI application, the endpoint URL is determined by your server's configuration (e.g., `http://your-server-ip:port/v1` or `http://localhost:port/v1/chat/completions`). You would get this from the team that set up the LLM or from the server's startup logs/documentation.
*   **Key Detail:** This URL often includes a version path, like `/v1`. It's crucial that this endpoint behaves like an OpenAI API endpoint.

### 2. An API Key for Your Custom Endpoint

*   **What it is:** An API key is like a secret password or token. It's a unique string of characters that your custom LLM service uses to verify that OpenHands (or any application) is authorized to make requests.
*   **Why it's needed:**
    *   **Security:** It prevents unauthorized access to your LLM, which might have usage costs or access to sensitive data.
    *   **Authentication:** It proves to the LLM service that the request is coming from a legitimate source (i.e., you or your application).
    *   **Rate Limiting/Billing (sometimes):** Some services use API keys to track usage for billing or to enforce request limits.
*   **Where to find it:**
    *   **Cloud LLM Providers:** Typically found in your provider's dashboard, under sections like "API Keys," "Credentials," or "Access Tokens."
    *   **Self-Hosted LLMs:** If your self-hosted LLM is configured to require an API key (a common practice for security), this key would have been defined during its setup. You might find it in a configuration file or it might have been provided to you by the setup team. For some local setups (like Ollama by default), an API key might not be strictly required, and often a placeholder like "NA" or "ollama" can be used, but this depends on the specific server configuration. *Always check your endpoint's documentation.*
*   **Important Note:** Treat your API keys like passwords. Keep them secure and do not share them publicly.

### 3. The Model Name Served by the Custom Endpoint

*   **What it is:** This is the specific identifier for the LLM you want to use that is being served at your custom endpoint URL. For example, even if your endpoint is `http://my-custom-llm.com/v1`, it might be capable of serving multiple models like `gpt-3.5-turbo`, `my-custom-llama-7b`, or `experimental-model-v3`.
*   **Why it's needed:** When OpenHands sends a request to your custom endpoint, it needs to specify *which model* hosted at that endpoint should process the request. The endpoint might be a gateway to several different LLMs.
*   **Where to find it:**
    *   **Cloud LLM Providers:** The model name (often called "deployment name" or "model ID") will be listed in your provider's dashboard, usually associated with the specific endpoint URL or deployed model instance.
    *   **Self-Hosted LLMs:**
        *   For tools like vLLM or TGI (Text Generation Inference), the model name is often related to the Hugging Face model path you used when starting the server (e.g., `meta-llama/Llama-2-7b-chat-hf` or a custom name you assigned).
        *   For Ollama, it's the model tag you pulled (e.g., `llama2` or `mistral`).
        *   If it's a truly custom API, the documentation or the team that built it will specify the acceptable model names.
*   **"OpenAI-Compatible" Implication:** When using an OpenAI-compatible endpoint, you often pass this model name in the API request body, similar to how you would with the official OpenAI API. Even if your custom endpoint only serves one model, you still typically need to provide its name.

---

By ensuring you have these three pieces of information, you'll be ready to configure OpenHands to leverage your custom LLM environment. Always refer to the documentation provided by your specific LLM service or the configuration of your self-hosted solution for the most accurate details.
