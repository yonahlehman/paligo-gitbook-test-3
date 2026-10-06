# AI Supply Chain Security

AI Supply Chain Security (AISC) provides clear insight into the AI components embedded throughout your software. As AI becomes a foundational part of modern development, it is increasingly difficult to know which models, agents, prompts, datasets, vector stores, and MCP components are present in your code or how they are being used. This lack of visibility creates Shadow AI inside the code itself, introducing untracked dependencies, unclear data flows, and compliance challenges.

AISC addresses this problem by discovering and classifying AI assets directly from your code and configuration. It detects a representative set of AI components, including:

- **MCP clients** : Detected via MCP client SDK usage, including imports, object instantiation, and method calls that establish connections to MCP servers.
- **MCP servers**: Detected via MCP server SDK implementations, including server initialization, tool/resource registration, and exposed handler methods.
- **AI agents**: Detected via agent frameworks and orchestration patterns (e.g., LangChain, Semantic Kernel, AutoGen, CrewAI), identified through framework imports, agent initialization, and workflow execution methods.
- **AI models** (pre-trained/fine-tuned): Recognized through standard loading calls and references to model artifacts or repositories.
- **AI Libraries (Core ML)**: Core ML frameworks (e.g., PyTorch, TensorFlow, scikit-learn).
- **AI SDKs**: Packages used to interact with LLM APIs and manage authentication, requests, streaming, and responses (e.g., OpenAI SDK, Anthropic SDK, Vertex AI libraries, Cohere client, Hugging Face Hub API clients).

With AISC, you gain the visibility needed to uncover hidden AI exposure, evaluate risk early, and apply governance with confidence, bringing transparency and control to your AI-enabled projects.

## In this section

- [Navigating AI Supply Chain Security](navigating-ai-supply-chain-security.md)
- [AI Supply Chain Security Configuration Options](ai-supply-chain-security-configuration-options.md)
- [LLM Risks Scanner](llm-risks-scanner.md)
