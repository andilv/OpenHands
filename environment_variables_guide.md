# Optional: Understanding Key Environment Variables for Advanced Configuration

While the OpenHands User Interface (UI) is the primary and recommended way for most users to configure their LLM settings, it's useful to know that OpenHands, primarily through its use of the LiteLLM library, may also recognize certain environment variables. These can be used for more advanced scenarios, for setting up configurations in environments where UI access is limited (e.g., server deployments), or potentially as overrides.

**Important Note:** UI settings within OpenHands are generally expected to take precedence over environment variables. However, this can sometimes depend on the specific implementation details of OpenHands and LiteLLM. Always refer to the official OpenHands documentation for the definitive behavior.

Below are some common LiteLLM environment variables that are relevant when working with OpenAI or custom OpenAI-compatible endpoints. Understanding these can be helpful for troubleshooting or specific deployment needs.

### Key Environment Variables

*   **`OPENAI_API_KEY`**
    *   **Purpose:** Sets the API key for OpenAI or an OpenAI-compatible endpoint.
    *   **Usage:** If the API key is not set in the UI, LiteLLM might pick it up from this environment variable if it's configured to manage an "OpenAI" provider type. This is a standard variable name used by many OpenAI client libraries.

*   **`OPENAI_API_BASE`** (or `AZURE_OPENAI_API_BASE`, `LITELLM_CUSTOM_LLM_API_BASE`)
    *   **Purpose:** Specifies the base URL for the OpenAI-compatible endpoint. This tells LiteLLM where to send the API requests, instead of the default OpenAI servers.
    *   **Usage:**
        *   `OPENAI_API_BASE`: Used if you're treating your custom endpoint as a direct override for the standard OpenAI provider.
        *   `AZURE_OPENAI_API_BASE`: Specifically for Azure OpenAI service.
        *   LiteLLM might also look for more generic variables like `LITELLM_CUSTOM_LLM_API_BASE` or provider-specific ones if you're defining a custom provider in code/config. The exact variable LiteLLM prioritizes can depend on its internal configuration and the "provider" name being used.
    *   This is essential for directing requests to your local Ollama instance, a corporate LLM gateway, or any other non-standard OpenAI endpoint.

*   **`OPENAI_API_VERSION`** (primarily for Azure OpenAI)
    *   **Purpose:** Specifies the API version required by the endpoint.
    *   **Usage:** This is particularly important for Azure OpenAI Service, which often requires a specific API version string (e.g., `2023-07-01-preview`). If OpenHands or LiteLLM needs to target an Azure endpoint, and this isn't configurable in the UI, this environment variable might be necessary.

*   **`LITELLM_MODEL_COST_MAP`**
    *   **Purpose:** Allows advanced users to define custom cost-per-token information for different models. LiteLLM can use this for logging and tracking expenses.
    *   **Usage:** This is more for users who are closely monitoring budget and usage across various models, especially custom or less common ones not already known to LiteLLM. For most users connecting to a single custom endpoint, this might not be immediately necessary but is good to be aware of for deeper LiteLLM integrations.
    *   **Format:** Typically a JSON string defining costs for input and output tokens for specified models.

### Important Considerations

*   **Documentation is Key:**
    *   **OpenHands Documentation:** The official OpenHands documentation is the primary source to understand which environment variables it specifically recognizes, their priority, and how they interact with UI settings. OpenHands might remap some LiteLLM variables or have its own specific set.
    *   **LiteLLM Documentation:** The LiteLLM documentation provides a comprehensive list of all environment variables it supports for various providers and general settings. This is invaluable if you're debugging connection issues or trying to achieve a very specific configuration.

*   **UI Precedence:** As mentioned, settings made directly in the OpenHands UI are generally intended to be the primary configuration method and may override environment variables. This is usually desirable for clarity and ease of management for most users.

*   **Specificity:** Some environment variables are very specific to the "provider" being configured in LiteLLM (e.g., variables prefixed with `AZURE_` are for Azure, `BEDROCK_` for AWS Bedrock, etc.). When using a custom OpenAI-compatible endpoint, you're often leveraging LiteLLM's generic OpenAI provider pathway or defining a custom one.

*   **Testing:** If you resort to using environment variables, ensure you have a way to test thoroughly to confirm they are being applied as expected and are not conflicting with UI configurations in an unintended way.

Using environment variables can offer flexibility for automated deployments or when fine-tuning behavior beyond standard UI options, but they should be approached with a clear understanding of how OpenHands and LiteLLM utilize them.
