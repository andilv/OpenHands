# Verification and Troubleshooting for Custom LLM Setup in OpenHands

After configuring OpenHands to use your custom OpenAI-compatible endpoint, it's crucial to verify that everything is working correctly. If you encounter issues, this guide provides general advice on how to troubleshoot them.

## 1. Verify the Connection

The simplest way to check if your setup is working is to try a basic interaction:

*   **Send a Test Prompt:** After saving your LLM configuration in the OpenHands UI, try giving it a simple prompt. For example:
    *   "Hello, who are you?"
    *   "What is 1+1?"
    *   "Tell me a short joke."
*   **Look for a Sensible Response:** If you receive a coherent and relevant answer from the LLM, your connection is likely established and working correctly!

## 2. General Troubleshooting Steps

If the test prompt fails or you suspect an issue, here’s how you can begin troubleshooting:

*   **Check OpenHands Logs:**
    *   **Where to find them:** OpenHands might display logs directly in its UI (e.g., in a console window or a dedicated "Logs" section) or store them in log files on your computer. Refer to OpenHands documentation for specific locations.
    *   **What to look for:** Scan the logs for error messages that occur after you try to use the LLM. Keywords or phrases to watch out for include:
        *   `LiteLLM error`: Indicates an issue happening within the LiteLLM library, which handles LLM communication.
        *   `HTTP status 401 Unauthorized` or `403 Forbidden`: Often points to an incorrect or missing API Key.
        *   `HTTP status 404 Not Found`: Could mean the Base URL is incorrect, the specific model path is wrong, or the model name isn't recognized by your endpoint.
        *   `HTTP status 500 Internal Server Error`: Suggests a problem on your custom endpoint's server side.
        *   `Connection refused` or `Connection timeout`: Indicates a network problem – OpenHands cannot reach your custom endpoint URL. The URL might be wrong, the server might be down, or a firewall could be blocking the connection.
        *   `Model not found` or `Invalid model`: The model name you specified in the OpenHands settings might be incorrect or not available at your custom endpoint.
        *   Error messages containing parts of your **Base URL** or **model name**.

*   **Check Your Custom Endpoint's Logs:**
    *   If you have access to the server running your custom LLM endpoint (e.g., if it's a self-hosted Ollama, vLLM, or a custom application), check its logs.
    *   These server-side logs can show if requests from OpenHands are even reaching your endpoint. They might also display more specific error messages about why a request failed (e.g., issues with the model loading, resource limits, etc.).

*   **Verify Network Connectivity:**
    *   Ensure the machine running OpenHands can network-reach your custom endpoint URL.
    *   **Ping the server:** If you know the IP address or hostname of your custom endpoint, try pinging it from the machine where OpenHands is running. (e.g., `ping your-llm-server-ip`).
    *   **Use `curl` (or a similar tool):** `curl` is a command-line tool to transfer data with URLs. This is an excellent way to test if the endpoint is reachable and if it's giving an expected (even if error) response.
        *   Open a terminal or command prompt on the machine running OpenHands.
        *   Try a command like: `curl http://your-custom-endpoint-url/v1/models` (The exact path `/v1/models` might vary, but it's a common one for OpenAI-compatible endpoints to list available models).
        *   If you need to include an API key for testing with `curl`, you might do something like: `curl -H "Authorization: Bearer YOUR_API_KEY" http://your-custom-endpoint-url/v1/models`
        *   A successful `curl` command that gets a JSON response (even an error JSON) means basic network connectivity is there. A "Connection refused" or "Host not found" directly from `curl` points to a network or URL issue.

## 3. Consult Official Documentation

If problems persist, these resources are your next best step:

*   **Official OpenHands Documentation:**
    *   Check the official documentation for OpenHands. Look for sections on LLM configuration, troubleshooting, or FAQs. There might be specific advice related to common issues or error codes encountered by OpenHands users.

*   **LiteLLM Documentation:**
    *   Since OpenHands uses LiteLLM under the hood, the LiteLLM documentation can be very helpful. It often contains detailed information about connecting to various LLM providers (including generic OpenAI-compatible endpoints), specific error codes, and advanced configuration options. You can find information on how LiteLLM interprets settings like `model`, `api_base`, and `api_key`.

By systematically checking these areas, you can often pinpoint the source of the problem and get your custom LLM integration with OpenHands working smoothly. Remember to double-check your entered settings for typos in the OpenHands UI as a first step!
