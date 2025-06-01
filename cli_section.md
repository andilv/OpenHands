## Configuring via Command Line Interface (CLI)

If you are using OpenHands primarily through its Command Line Interface (CLI), you have several ways to configure it for a custom OpenAI-compatible endpoint.

### 1. Using Environment Variables (Recommended for CLI)

Setting environment variables is often the most straightforward method for CLI usage, especially when running OpenHands in scripts, automated workflows, or Docker containers. OpenHands, largely through LiteLLM, typically recognizes the following key variables:

*   **`LLM_MODEL`**: Specifies the model to be used.
    *   **Format:** `openai/<your-custom-model-name>`
    *   **Example:** `openai/my-llama3-8b-instruct`, `openai/gpt-4o-mini`
    *   **Note:** The `openai/` prefix is a convention used by LiteLLM to indicate that the model, even if custom, expects to communicate using the OpenAI API structure. Replace `<your-custom-model-name>` with the actual model identifier from your endpoint.

*   **`LLM_API_KEY`**: Your API key for the custom endpoint.
    *   **Example:** `your_api_key_here`, or a placeholder like `NA` or `ollama` if your endpoint doesn't require a key (always check your endpoint's documentation).

*   **`LLM_BASE_URL`** (or **`OPENAI_API_BASE`**): The full base URL of your custom OpenAI-compatible endpoint.
    *   **Example:** `http://localhost:11434/v1`, `https://api.mycustomllm.com/v1/chat/completions`
    *   **Note:** While `LLM_BASE_URL` is a common environment variable name, LiteLLM (which OpenHands uses for LLM connections) also often respects `OPENAI_API_BASE`. If one doesn't seem to work, try the other. Consult the OpenHands or LiteLLM documentation for the exact variable names they prioritize.

**Conceptual Example:**

You would set these environment variables in your terminal session *before* running the OpenHands CLI command.

```bash
# Set the environment variables
export LLM_MODEL="openai/my-custom-model"
export LLM_API_KEY="your_very_secret_api_key"
export LLM_BASE_URL="http://localhost:11434/v1" # Example for a local Ollama endpoint

# Then run your OpenHands CLI command
# The actual command might vary based on your setup (e.g., poetry, direct script execution)
# poetry run python -m openhands.cli.main --task "Summarize the content of example.txt"
```

For **Docker containers**, you would pass these environment variables using the `-e` flag:

```bash
docker run --rm -it \
  -e LLM_MODEL="openai/my-custom-model" \
  -e LLM_API_KEY="your_very_secret_api_key" \
  -e LLM_BASE_URL="http://host.docker.internal:11434/v1" # Example for Ollama on host
  # Add other necessary volume mounts or configurations
  openhands_image_tag # Replace with your OpenHands Docker image
  # Command to run inside the container, e.g.:
  python -m openhands.cli.main --task "What is the capital of France?"
```

### 2. Using the Interactive `/settings` Command

If you are running the OpenHands CLI in its interactive mode (e.g., by launching `python -m openhands.cli.main` without a specific task), you can configure settings dynamically:

1.  **Start the CLI:** Launch the OpenHands interactive CLI.
    ```bash
    poetry run python -m openhands.cli.main
    ```
2.  **Access Settings:** Once the CLI is running and you see its prompt, type `/settings` and press Enter.
3.  **Follow Prompts:** The CLI will guide you through the available settings. Look for options related to:
    *   LLM Provider (you might select "OpenAI" or a custom option)
    *   Model Name (enter in `openai/<your-model-name>` format)
    *   API Key
    *   Base URL (Endpoint URL)
    *   You may need to enable "Advanced settings" or navigate to a specific sub-menu for LLM configuration.
4.  **Save Changes:** Ensure you save the settings as prompted. This process is similar to configuring via the UI but is entirely text-based within your terminal.

### 3. Using `config.toml` (Local Python Setups)

For local Python installations (not Docker), OpenHands often uses a `config.toml` file to store persistent configuration settings. You can typically define your LLM provider, model, API key, and base URL directly in this file.

*   **Location and Structure:** The exact location and expected structure of `config.toml` can vary. Please refer to the official OpenHands documentation for details on where to find this file (it might be in a directory like `~/.config/openhands/` or within the project directory) and the correct TOML syntax for defining your custom LLM endpoint.

This method is useful if you prefer not to set environment variables every time or if you want a more permanent configuration for a specific local setup. UI and `/settings` changes might also get reflected here.
