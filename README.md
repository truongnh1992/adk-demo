# Multi-Tool Agent

A sophisticated multi-agent system built with Google's Agent Development Kit (ADK) that demonstrates agent orchestration, tool usage, and specialized task delegation.

## Overview

This project showcases a hierarchical agent architecture where a root coordinator agent manages specialized sub-agents, each with their own tools and responsibilities:

- **Root Agent**: Coordinates between sub-agents and handles weather requests
- **Greeting Agent**: Specialized for handling user greetings
- **Farewell Agent**: Specialized for handling user farewells
- **Weather Tool**: Provides weather information for various cities

## Features

- 🌤️ **Weather Information**: Get current weather for major cities
- 👋 **Smart Greetings**: Personalized greeting messages
- 👋 **Polite Farewells**: Courteous goodbye messages
- 🤖 **Agent Orchestration**: Intelligent delegation between specialized agents
- 🔧 **Tool Integration**: Seamless tool usage across agents

## Architecture

```
Root Agent (weather_agent_team)
├── Weather Tool (get_weather)
├── Greeting Agent
│   └── Say Hello Tool (say_hello)
└── Farewell Agent
    └── Say Goodbye Tool (say_goodbye)
```

## Setup

### Prerequisites

- Python 3.8+
- Google ADK installed
- Valid API key for the model (Gemini 2.5 Flash)

### Installation

1. Clone the repository:
   ```bash
   git clone <repository-url>
   cd multi_tool_agent
   ```

2. Install dependencies:
   ```bash
   pip install google-adk
   ```

3. Set up your environment variables:
   ```bash
   # Create .env file with your API key
   echo "GOOGLE_API_KEY=your_api_key_here" > .env
   echo "GOOGLE_GENAI_USE_VERTEXAI=FALSE" > .env
   ```

### Configuration

The project uses `gemini-2.5-flash` as the default model. You can modify the `AGENT_MODEL` variable in `agent.py` to use different models.

## Usage

### Running the Agent

Start the web interface:
```bash
adk web
```

The agent will be available at the provided URL (typically `http://localhost:8000`).

### Interacting with the Agent

The agent can handle various types of requests:

#### Weather Queries
- "What's the weather in London?"
- "How's the weather in Tokyo?"
- "Tell me about the weather in Hanoi"

#### Greetings
- "Hi"
- "Hello"
- "Hello, my name is John"

#### Farewells
- "Bye"
- "Goodbye"
- "See you later"

### Available Cities

The weather tool currently supports:
- Hanoi
- London
- Tokyo

## Tools

### Weather Tool (`get_weather`)
- **Purpose**: Retrieve weather information for specified cities
- **Input**: City name (string)
- **Output**: Weather report or error message

### Greeting Tool (`say_hello`)
- **Purpose**: Generate personalized greetings
- **Input**: Name (optional)
- **Output**: Friendly greeting message

### Farewell Tool (`say_goodbye`)
- **Purpose**: Generate polite farewell messages
- **Input**: None
- **Output**: Goodbye message

## Agent Behavior

The root agent intelligently analyzes user queries and:

1. **Delegates to Greeting Agent** for greeting-related queries
2. **Delegates to Farewell Agent** for farewell-related queries
3. **Handles weather requests directly** using the weather tool
4. **Responds appropriately** to other queries or states limitations

## Development

### Adding New Cities

To add support for more cities, modify the `mock_weather_db` dictionary in the `get_weather` function:

```python
mock_weather_db = {
    "hanoi": {"status": "success", "report": "The weather in Ha Noi is sunny with a temperature of 25°C."},
    "london": {"status": "success", "report": "It's cloudy in London with a temperature of 15°C."},
    "tokyo": {"status": "success", "report": "Tokyo is experiencing light rain and a temperature of 18°C."},
    "newyork": {"status": "success", "report": "New York is clear with a temperature of 22°C."},  # Add new cities here
}
```

### Adding New Tools

1. Define your tool function
2. Add it to the appropriate agent's `tools` list
3. Update the agent's instructions to include usage of the new tool

### Adding New Agents

1. Create the agent with specific instructions and tools
2. Add it to the root agent's `sub_agents` list
3. Update the root agent's instructions to include delegation logic

## Error Handling

The system includes comprehensive error handling:

- **Missing API Keys**: Graceful degradation with clear error messages
- **Unknown Cities**: Polite error responses for unsupported locations
- **Agent Failures**: Fallback behavior when sub-agents fail to initialize

## Logging

The project includes detailed logging for:
- Tool execution tracking
- Agent creation status
- Error diagnostics

## License

This project is for educational and demonstration purposes.

## Contributing

Feel free to submit issues and enhancement requests! 