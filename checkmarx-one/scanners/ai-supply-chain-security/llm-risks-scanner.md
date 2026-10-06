# LLM Risks Scanner

This page describes what the LLM Risk Scanner analyses, which risk categories it detects, how detection works, and what the scan output contains. It also covers current model coverage and upcoming enhancements.

## What the Scanner Analyses

The scanner inspects both source code and binary model artifacts to surface risks at two layers:

- **AI technology inventory** - which models, frameworks, SDKs, and agents are present in the codebase
- **Security risk patterns** - code and artifact-level patterns that can lead to remote code execution (RCE), supply-chain compromise, or policy violations

### AI Technology Inventory

The scanner performs automatic discovery of AI components across the codebase. Detected categories include:

| Category | What is detected | Examples |
|---|---|---|
| AI Models | Specific LLM identifiers referenced in code, configuration, or scripts | GPT-4o, Claude Sonnet 4.5, Llama 3.3 70B, Gemini 2.5 Pro |
| AI Frameworks & Libraries | ML framework imports and usage patterns | PyTorch, TensorFlow, Keras, Hugging Face Transformers, scikit-learn |
| AI Agents | Agent framework instantiation and orchestration patterns | CrewAI, AutoGen, LangChain, LangGraph, Semantic Kernel |
| AI SDKs | Official provider client libraries and their usage | OpenAI SDK, Anthropic SDK, Azure AI SDK, Google GenAI SDK |
| MCP Clients & Servers | Model Context Protocol integrations that connect LLMs to external systems | MCP client sessions, FastMCP servers, tool registrations |

### Security Risk Detection

Beyond inventory, the scanner checks for patterns that are commonly exploited in ML supply-chain attacks. All risk findings are severity-rated and include remediation guidance.

## Detected Risk Categories

The following risk categories are currently detected. Each finding includes a severity rating, the specific sink or pattern triggered, affected file types, and recommended remediation.

| Risk Category | Severity | What it means |
|---|---|---|
| Malicious Pickle / Torch Gadget Patterns | Critical | Model or pickle files contain opcodes that can execute arbitrary code when deserialised. Direct RCE risk. |
| Unsafe Deserialization in Code | Critical | Code uses pickle, joblib, dill, cloudpickle, or unsafe YAML APIs on potentially untrusted data - a classic RCE vector. |
| Unsafe Model Deserialization (PyTorch / TF / Keras / FastAI) | Critical | Model loaders such as `torch.load` or `tf.keras.models.load_model` can execute code during loading when given untrusted artifacts. |
| Direct OS Command Execution | Critical | Code or serialised artifacts invoke `os.system, subprocess.Popen`, or equivalent calls enabling full OS-level compromise. |
| Dynamic Code Evaluation | Critical | `eval / exec / execfile` patterns in code or artifacts that can run arbitrary logic if influenced by untrusted input. |
| Trust-Remote-Code Flags | High | `trust_remote_code=True` downloads and runs Python code from a model repository at load time, turning "model loading" into remote code execution if the repo is compromised. |
| Remote Model Download and Execution from Hubs | High | Automated download-and-load flows (e.g. `huggingface_hub.snapshot_download`) that can pull unsafe serialised formats or repository-provided code without adequate validation gates. |
| Dangerous Keras / TF Lambda and PyFunc Callbacks | High | Lambda layers or `tf.py_function` ops embed arbitrary Python functions in the computation graph. These are executed at inference time, not just at load time. |
| Executable Layers in Keras / HDF5 Model Files | High | Binary model files (`.h5, .keras, .pb`) contain Lambda or equivalent executable layers that can run Python on deserialisation. |
| Auto-Loading from JSON / Config (AutoModel / AutoTokenizer) | Medium | Configuration files can silently trigger automatic model downloads and code instantiation via AutoModel or AutoTokenizer patterns. |
| Forced Non-Interactive Execution Flags | Medium | Scripts or commands use `-y`, `--force`, or equivalent flags that bypass interactive safety checks, removing the last human-approval gate in CI pipelines. |

## How Detection Works

The scanner uses a multi-signal strategy to ensure high precision and low false-positive rates.

### Model & Technology Detection

- **Import detection** - identifies package imports across Python, JavaScript, Go, Java, and C# source files.
- **Usage confirmation** - requires both an import statement and a corresponding class instantiation or API call. This avoids false positives from unused dependencies or commented-out code.
- **Exact string matching for AI models** - model identifiers such as `gpt-4o` or `claude-3-5-sonnet-20241022` are matched wherever they appear: API call parameters, environment variables, configuration files, and shell scripts.

### Risk Pattern Detection

- **Source code analysis** - Python and notebook files are scanned for dangerous sink functions and dangerous API patterns.
- **Binary artifact inspection** - model files (`.pkl, .pt, .pth, .h5, .keras, .pb, .bin`) are inspected directly for embedded opcodes, executable graph components, and suspicious serialisation patterns. No execution is performed.
- **Configuration file analysis** - JSON and YAML configuration files are checked for patterns that drive unsafe automatic loading behavior.

{% hint style="info" %}
The scanner does not execute any model file or code during analysis. All binary inspection is performed through static analysis only.
{% endhint %}

## Model Coverage

The scanner currently detects **528+ AI models** across all major providers and deployment platforms.

| Provider / Platform | Coverage |
|---|---|
| OpenAI | All GPT-4, GPT-4o, GPT-4.1, GPT-5, o1, o3, o4 families and variants |
| Anthropic | All Claude 3, 3.5, 3.7, Opus 4 / Sonnet 4 / Haiku 4 families |
| Google | Gemini 1.5, 2.0, 2.5, 3.0 families; Gemma open-weight models |
| Meta | Llama 2, 3, 3.1, 3.2, 3.3, 4 families (Hugging Face and AWS Bedrock) |
| Mistral AI | Mistral, Mixtral, Pixtral, Magistral, Codestral, Ministral families |
| Microsoft | Phi 1.5 through Phi 4 families; Azure AI hosted models |
| DeepSeek | R1, V3, V3.2 families including distilled variants |
| AWS Bedrock | Amazon Nova, Titan, and all third-party models hosted on Bedrock |
| Azure AI | Models from Azure AI marketplace across all hosted providers |
| Hugging Face | Top open-weight models by adoption including Qwen, Falcon, Bloom, and more |
| Other providers | Cohere, xAI (Grok), NVIDIA Nemotron, Moonshot AI (Kimi), MiniMax, and others |

Model coverage is continuously updated. New model families are added on an ongoing basis as providers release new versions.

## What You Get in the Scan Output

### AI Component Inventory

A complete list of AI models, frameworks, SDKs, agents, and MCP integrations detected in the scanned codebase or repository, including:

- The specific model version or identifier found
- The file path and line number where it was referenced
- The provider and hosting platform (e.g. AWS Bedrock, Azure AI, Hugging Face)
- Lifecycle state - whether the model is currently active or deprecated

### Risk Findings

For each detected risk pattern, the output includes:

- Risk category and severity (Critical / High / Medium)
- Specific sink or pattern that was triggered
- Affected file path and line number
- Concise explanation of the risk and why it matters
- Actionable remediation guidance

### CycloneDX Export

Scan results are exportable in CycloneDX 1.7 SBOM format, using the machine-learning-model component type. Each model entry in the BOM includes:

- Model identity, provider, version, and aliases
- Hosting platform and license information
- Scan evidence - file path, line, and detection technique
- Enrichment fields such as context window size and lifecycle state, where available

## Scan Modes

The scanner supports different scan modes that control the scope of files analysed. Broader scan modes provide more comprehensive coverage but may take longer to complete. Quick Scan is available today; Smart Scan and Deep Scan are planned for future releases.

| Scan mode | Availability | What is scanned |
|---|---|---|
| Quick Scan | Available | All model and code files under 10 MB, scanned for vulnerabilities |
| Smart Scan | Planned | All files up to 10 MB plus all pickle files regardless of size |
| Deep Scan | Planned | All files with no size restriction |

## Supported File Types

| File type | Examples | What is checked |
|---|---|---|
| Shell scripts | .sh | OS command execution, force-flag patterns, hub download calls |
| Python source | .py, .ipynb | Imports, API calls, dangerous sink functions, eval/exec patterns |
| Documentation / Markdown | .md | Embedded code snippets, model identifiers, command examples |
| Pickle and serialised artifacts | .pkl, .pickle, .pcl | Pickle opcodes, GLOBAL/REDUCE patterns, gadget chains |
| PyTorch checkpoints | .pt, .pth | Torch rebuild helpers, serialised Python objects |
| Keras / TensorFlow models | .h5, .keras, .pb | Lambda layers, PyFunc ops, unsafe deserialisation paths |
| Generic binary model files | .bin, .dat, .data, .raw, .model | Embedded pickle or executable patterns |
| Configuration files | config.json, tokenizer_config.json | AutoModel / AutoTokenizer patterns, remote-code triggers |

## Upcoming Enhancements

Checkmarx continuously expands scanner capabilities. Planned enhancements include:

- **Expanded model registry** - growing from 528 to ~22,000 tracked models across all major providers, open-weight hubs, and deployment marketplaces, after cross-source deduplication.
- **Enriched model cards** - adding lifecycle state and deprecation dates, context window and output limits, pricing data, and third-party benchmark scores to each detected model, enabling risk-informed decisions about which models are in use.
- **Broader platform coverage** - extending collection to include OpenRouter, Artificial Analysis benchmarking data, and additional Hugging Face open-weight models ranked by real-world adoption.
- **CycloneDX BOM enrichment** - populating additional SBOM fields automatically from the expanded model registry, so your AI SBOM reflects current model metadata without manual curation.

Coming in 2026: Enhanced model registry with ~22,000+ tracked models, enriched metadata, and expanded CycloneDX BOM output.
