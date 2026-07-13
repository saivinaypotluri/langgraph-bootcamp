# LangGraph Tutorial

This project is a comprehensive tutorial on `langgraph`, a library for building stateful, multi-agent applications with LLMs. The tutorial is presented as a series of Jupyter notebooks, each of which covers a different aspect of `langgraph`.

For a detailed developer's journal, including a breakdown of the libraries used and diagrams of the graphs built, please see [JOURNAL.md](JOURNAL.md).

## Getting Started

### Prerequisites

*   Python 3.12 or higher
*   An API key for Google's Generative AI.

### Setup and Installation

This project uses `uv` for fast dependency management and environment creation.

1.  **Install `uv`**:
    If you don't have `uv` installed, you can install it with:
    ```bash
    pip install uv
    ```

2.  **Clone the Repository**:
    ```bash
    git clone https://github.com/saivinaypotluri/langgraph-bootcamp.git
    cd langgraph-tutorial
    ```

3.  **Sync Dependencies**:
    This command will create a virtual environment (`.venv`) and install all the necessary packages from `pyproject.toml` and `uv.lock`.
    ```bash
    uv sync
    ```

4.  **Set Up Environment Variables**:
    Create a `.env` file in the root of the project and add your Google API key.
    ```
    cp .env.example .env
    GOOGLE_API_KEY="YOUR_API_KEY"
    ```
    The application will load this key automatically.

5.  **Run the Jupyter Notebooks**:
    You can run Jupyter Notebook from within the `uv`-managed environment.
    ```bash
    uv run jupyter notebook
    ```
    This ensures you are using the packages you just installed. Alternatively, you can activate the environment first:
    ```bash
    # macOS / Linux
    source .venv/bin/activate

    # Windows
    .venv\Scripts\activate

    # Then run jupyter
    jupyter notebook
    ```

## Key Libraries and Modules

| Library | Purpose | Key Modules & What They Do |
| :--- | :--- | :--- |
| `langgraph` | The core library for building stateful, multi-agent applications with cyclical workflows. It extends LangChain by allowing graphs to have loops, which is essential for agentic behavior like reasoning and self-correction. | **`graph.StateGraph`**: The main class to define a new stateful graph. It takes a state schema and allows you to add nodes and edges. <br> **`graph.START`, `graph.END`**: Special identifiers for the entry and exit points of the graph, making the flow explicit. |
| `langchain_core`| Provides the foundational data structures and abstractions for the entire LangChain ecosystem. It ensures a standard way to represent messages, prompts, and runnable components. | **`messages.AIMessage`, `HumanMessage`, etc.** Classesto represent different roles in a conversation (AI, user, system). This is crucial for the LLM to understand context. <br> **`prompts.PromptTemplate`**: A tool for creating dynamic and reusable prompts that can be populated with variables at runtime. |
| `langchain_google_genai` / `langchain_openai` | These are provider-specific packages that act as a bridge to the actual LLM APIs (Google Gemini, OpenAI GPT). They handle authentication, request formatting, and response parsing. | **`chat_models.ChatGoogleGenerativeAI`**: The specific class used to instantiate and interact with Google's Gemini chat models. |
| `pydantic` | Used for data validation and settings management using Python type annotations. It ensures the state object flowing through the graph is always well-structured and valid, preventing runtime data errors. | **`BaseModel`**: The base class you inherit from to create your own custom, validated data models. <br> **`Field`**: Used within a `BaseModel` to provide extra configuration, such as descriptions or validation for a specific field. |
| `python-dotenv` | A simple library for managing environment variables. It's used as a best practice to keep sensitive data like API keys out of your source code by loading them from a `.env` file. | **`load_dotenv`**: A function that you call at the start of your application to load the variables from the `.env` file into the process's environment. |
| `typing` | The built-in Python library for type hints. It's used to make the code more readable, self-documenting, and allows static analysis tools to catch potential errors before runtime. | **`TypedDict`**: A way to define a dictionary schema with specific keys and value types. <br> **`List`**: The standard way to denote a list of a certain type. <br> **`Annotated`**: Allows attaching metadata to types, used here with a reducer function (`add`) for automatic message list management in the graph's state. |

## Notebooks

1.  **1_basics.ipynb:** Introduction to `langgraph`, setting up the environment, and creating a simple graph.
2.  **2_Pydantic.ipynb:** Using Pydantic models to define the state of the graph.
3.  **3_messages.ipynb:** Handling messages (Human, AI, System, Tool) in `langgraph`.
4.  **4_Prompts&Chains.ipynb:** Using prompts and chains in `langgraph`.
5.  **5_Tools&Binding.ipynb:** Using tools and binding them to the graph.
6.  **6_ReAct.ipynb:** Implementing a ReAct agent.
7.  **7_Parallelization.ipynb:** Running nodes in parallel.
8.  **8_Router.ipynb:** Routing the flow of the graph based on conditions.
9.  **9_Orchestrator_Worker.ipynb:** Creating a master-worker setup.
10. **10_Generator_Evaluator.ipynb:** Creating a generator-evaluator setup.
11. **11_Memory.ipynb:** Adding memory to the graph.
12. **12_HumanInLoop.ipynb:** Adding a human-in-the-loop to the graph.
