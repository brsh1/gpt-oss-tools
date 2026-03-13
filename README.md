# Iris — Your day, made easy (Ollama Optimized)

Iris is your intelligent assistant combining advanced reasoning with local, privacy-first tools. Refactored specifically for the **gpt-oss** model on **Ollama**, Iris now uses native tool-calling formats for even better reliability.

## **Key Features**

- **Optimized for gpt-oss** — Leverages the native `functions` namespace and reasoning capabilities of the gpt-oss model family.
- **Real-time web intelligence** — Search the web and browse detailed content.
- **Weather at a glance** — Automatic location detection and accurate forecasts from weather.gov.
- **Stock Market Insights** — Fetch live prices and daily moves.
- **Secure Python Execution** — Run calculations and data processing in a safe sandbox.
- **Calendar Management** — Full Google Calendar integration (list, create, delete).
- **Scheduled Tasks** — Create one-time or recurring tasks that persist across sessions.
- **Privacy First** — Runs entirely on your local machine via Ollama.

## **Quick Start with Ollama & gpt-oss**

### 1. Prerequisites
- [Ollama](https://ollama.com/) installed and running.
- Python 3.10+ (3.13 recommended).

### 2. Setup Environment
```bash
# Create and activate virtual environment
uv venv env --python 3.13
source env/bin/activate

# Install dependencies
uv pip install -r requirements.txt
```

### 3. Build the Iris Model
Iris uses a custom `Modelfile` to define its tools and instructions for gpt-oss.
```bash
# Pull the base model if you haven't already
ollama pull gpt-oss:20b

# Create the Iris model
ollama create iris -f Modelfile
```

### 4. Configure Google Calendar (Optional)
Place your `credentials.json` in the project root and run:
```bash
python generateToken.py
```

### 5. Launch Iris
Iris can be run as an interactive chat, a single-shot command, or a web UI. It does **not** need to run in the background; tasks are checked whenever you launch the assistant.

- **Interactive CLI:**
  ```bash
  python gpt-oss-tools.py --model iris
  ```
- **Single-shot Command (On-demand):**
  ```bash
  python gpt-oss-tools.py --model iris --query "What is the weather in NYC?"
  ```
- **Web UI:**
  ```bash
  python gpt-oss-tools.py --web --model iris
  ```

## **Using gpt-oss with Tools**

Iris is designed to work best with `gpt-oss:20b` or `gpt-oss:120b`. By using the `Modelfile`, we instruct the model on exactly how to use its native "commentary" channel to call local Python functions.

### **Pro Tips for gpt-oss**
- **Reasoning:** Iris sets the reasoning effort to `high` in the Modelfile. This allows the model to think through complex tool use cases before responding.
- **Context:** The context window is expanded to 32k tokens to handle long web browsing results and chat history.
- **Formatting:** gpt-oss is excellent at Markdown. It will automatically format tables, code blocks, and bold text for high readability.

## **Toolbox Reference**

| Category | Tool | Description |
| :--- | :--- | :--- |
| **Search** | `web_search`, `browse_url` | Find information and read full webpage content. |
| **Weather** | `get_location`, `get_weather` | Get local forecasts based on IP. |
| **Stock** | `get_stock_price` | Check ticker symbols for live pricing. |
| **Python** | `execute_python` | Run code for math and data logic. |
| **Calendar**| `list_calendar_events`, `create_calendar_event` | Manage your Google Calendar events. |
| **Tasks** | `schedule_task`, `check_tasks` | Set reminders or recurring agentic actions. |

---
*Note: Smart home (lights) functionality has been removed in this version to focus on core productivity and agentic reasoning.*
