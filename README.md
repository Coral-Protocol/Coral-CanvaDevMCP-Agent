## [Canva Dev MCP Agent](https://github.com/Coral-Protocol/Coral-CanvaDevMCP-Agent)

The Canva Dev MCP Agent is capable of accessing and interpreting Canva's developer documentation, SDKs, UI kits, and design guidelines to assist in creating, understanding, and reviewing Canva apps and integrations.

## Responsibility

The Canva Dev MCP Agent is capable of retrieving comprehensive documentation from Canva's developer ecosystem, including Connect documentation, Apps SDK, UI Kit components, design guidelines, and CLI documentation. It can provide design review instructions and app creation guidance tailored to Canva's development standards.

Below are the tools and their descriptions:

**read-canva-connect-documentation-index**: This tool reads the Canva Connect documentation index to provide access to integration and API documentation. Usage: Ask "Show me the Connect documentation index" or "What's available in Canva Connect docs" to explore the available integration resources.

**read-canva-apps-sdk-documentation-index**: This tool reads the Canva Apps SDK documentation index to provide access to app development resources. Usage: Ask "Show me the Apps SDK documentation index" or "What's available in the Canva Apps SDK" to explore app development resources.

**read-canva-documentation-pages**: This tool fetches specific Canva documentation pages by providing URLs. Usage: Ask "Get documentation for these URLs: [url1, url2]" or "Read these specific Canva docs: [list of URLs]" to retrieve targeted documentation content.

**read-canva-app-ui-kit-index**: This tool reads the Canva App UI Kit index to provide access to UI components and patterns. Usage: Ask "Show me the UI Kit index" or "What UI components are available" to explore the available UI resources.

**read-canva-app-ui-kit-patterns-catalog**: This tool reads the Canva App UI Kit patterns catalog to provide access to design patterns and best practices. Usage: Ask "Show me the UI patterns catalog" or "What design patterns are available" to explore UI design patterns.

**read-canva-app-ui-kit-page**: This tool reads specific UI kit pages with component props and metadata. Usage: Ask "Get UI kit page for component X" or "Show me the props for Button component" to retrieve detailed component information. Requires project_root and props_metadata parameters.

**read-canva-cli-documentation**: This tool reads Canva CLI documentation to provide command-line interface guidance. Usage: Ask "Show me CLI documentation" or "What CLI commands are available" to explore command-line tools.

**read-canva-apps-sdk-design-guidelines**: This tool reads Canva Apps SDK design guidelines to provide best practices and design standards. Usage: Ask "Show me design guidelines" or "What are the design best practices" to explore design standards.

**design-review-instructions**: This tool provides design review instructions and guidance for Canva apps. Usage: Ask "How do I review a Canva app design" or "Give me design review guidelines" to get review instructions.

**create-canva-app-instructions**: This tool provides instructions for creating Canva apps. Usage: Ask "How do I create a Canva app" or "Give me app creation instructions" to get development guidance.

## Details
- **Framework**: LangChain
- **Tools used**: Canva Dev MCP Server Tools, Coral Server Tools
- **AI model**: OpenAI GPT-4.1-mini
- **Date added**: December 2024
- **Reference**: [Canva Developer Platform](https://www.canva.dev/)
- **License**: MIT

## Setup the Agent

### 1. Clone & Install Dependencies

<details>

Ensure that the [Coral Server](https://github.com/Coral-Protocol/coral-server) is running on your system. If you are trying to run Canva Dev agent and require an input, you can either create your agent which communicates on the coral server or run and register the [Interface Agent](https://github.com/Coral-Protocol/Coral-Interface-Agent) on the Coral Server  

```bash
# In a new terminal clone the repository:
git clone https://github.com/Coral-Protocol/Coral-CanvaDevMCP-Agent.git

# Navigate to the project directory:
cd Coral-CanvaDevMCP-Agent

# Download and run the UV installer, setting the installation directory to the current one
curl -LsSf https://astral.sh/uv/install.sh | env UV_INSTALL_DIR=$(pwd) sh

# Create a virtual environment named `.venv` using UV
uv venv .venv

# Activate the virtual environment
source .venv/bin/activate

# install uv
pip install uv

# Install dependencies from `pyproject.toml` using `uv`:
uv sync
```

</details>

### 2. Configure Environment Variables

<details>

Get the API Key:
[OpenAI](https://platform.openai.com/api-keys)

```bash
# Create .env file in project root
cp -r .env_sample .env
```

Check if the .env file has correct URL for Coral Server and adjust the parameters accordingly.

</details>

## Run the Agent

You can run in either of the below modes to get your system running.  

- The Executable Model is part of the Coral Protocol Orchestrator which works with [Coral Studio UI](https://github.com/Coral-Protocol/coral-studio).  
- The Dev Mode allows the Coral Server and all agents to be separately running on each terminal without UI support.  

### 1. Executable Mode

Checkout: [How to Build a Multi-Agent System with Awesome Open Source Agents using Coral Protocol](https://github.com/Coral-Protocol/existing-agent-sessions-tutorial-private-temp) and update the file: `coral-server/src/main/resources/application.yaml` with the details below, then run the [Coral Server](https://github.com/Coral-Protocol/coral-server) and [Coral Studio UI](https://github.com/Coral-Protocol/coral-studio). You do not need to set up the `.env` in the project directory for running in this mode; it will be captured through the variables below.

<details>

For Linux or MAC:

```bash
# PROJECT_DIR="/PATH/TO/YOUR/PROJECT"

applications:
  - id: "app"
    name: "Default Application"
    description: "Default application for testing"
    privacyKeys:
      - "default-key"
      - "public"
      - "priv"

registry:
  canva_dev_mcp_agent:
    options:
      - name: "API_KEY"
        type: "string"
        description: "API key for the service"
    runtime:
      type: "executable"
      command: ["bash", "-c", "${PROJECT_DIR}/run_agent.sh main.py"]
      environment:
        - name: "API_KEY"
          from: "API_KEY"
        - name: "MODEL_NAME"
          value: "gpt-4.1-mini"
        - name: "MODEL_PROVIDER"
          value: "openai"
        - name: "MODEL_TOKEN"
          value: "8000"
        - name: "MODEL_TEMPERATURE"
          value: "0.1"

```

For Windows, create a powershell command (run_agent.ps1) and run:

```bash
command: ["powershell","-ExecutionPolicy", "Bypass", "-File", "${PROJECT_DIR}/run_agent.ps1","main.py"]
```

</details>

### 2. Dev Mode

Ensure that the [Coral Server](https://github.com/Coral-Protocol/coral-server) is running on your system and run below command in a separate terminal.

<details>

```bash
# Run the agent using `uv`:
uv run python main.py
```

You can view the agents running in Dev Mode using the [Coral Studio UI](https://github.com/Coral-Protocol/coral-studio) by running it separately in a new terminal.

</details>

## Example

<details>

```bash
# Input:
Canva Dev MCP instruction - "Show me the UI Kit index and available components"

# Output:
The agent will retrieve and display the Canva App UI Kit index, showing all available UI components and their descriptions for app development.
```

</details>

### Creator Details
- **Name**: Mustafa Khan
- **Affiliation**: Coral Protocol
- **Contact**: [Discord](https://discord.com/invite/Xjm892dtt3)
