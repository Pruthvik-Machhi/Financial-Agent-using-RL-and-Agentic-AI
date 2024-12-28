# **Financial Insights Using RL & Agentic AI**

### **Overview**

#### **Reinforcement Learning**
- Develop a trading strategy using a Deep Q-Network (DQN) to maximize profit.
  - Autonomous decision-making for buy, sell, and hold actions based on stock data.
  - Requires no pre-defined strategy; the model learns optimal policies through exploration.
- Demonstrates the potential of RL in dynamic, data-driven trading environments focused on autonomous learning.

---

#### **Agentic AI**
-  Enhance trading decisions with modular AI agents for external data integration and insights.which includes,
  - **Web Search Agent**: Retrieves real-time stock news and contextual information using DuckDuckGo.
  - **Finance AI Agent**: Gathers stock prices, analyst recommendations, fundamentals, and news using YFinance.
  - **Multi-Agent Collaboration**: Combines insights for comprehensive financial analysis and decision-making.
  - Built on Groq models (LLaMA 3), with easy-to-use tools and interactive Playground deployment.
  - Outputs formatted with tables and sources for clarity and reliability.
- A flexible, multi-agent system that complements RL strategies with external data and insights leveraging modular AI agents for informed decision-making. 

--- 
## **RL Agent**

In your project, the **Reinforcement Learning (RL) agent** is designed to make trading decisions based on market data and optimize its actions for maximum profit.

#### **1. Environment Setup**
The RL agent interacts with a simulated environment where it makes decisions (buy, sell, or hold) based on the current market state. The environment provides the agent with feedback (reward or penalty) after each action, allowing the agent to learn and improve its strategy over time.

#### **2. Configuration**
- **State Space**: The state represents information about the market, such as stock prices, technical indicators, and other relevant features.
- **Action Space**: The actions the agent can take are typically buy, sell, or hold positions.
- **Reward Function**: The agent receives a reward (or penalty) based on the profit or loss made from its action. Positive rewards encourage profitable actions, while negative rewards discourage unprofitable actions.
- **Model**: The RL agent uses **Deep Q-Learning (DQN)**, which is a neural network-based method. It approximates the Q-values (expected future rewards) for each state-action pair to guide decision-making.

#### **3. Working**
- The RL agent starts with random exploration, trying various actions and receiving feedback from the environment.
- Over time, the agent learns the most effective trading strategies by updating its Q-values based on the rewards it receives after each action.
- The agent’s goal is to maximize its total profit over time by continuously improving its policy.

This RL agent learns to maximize profits by trading in the simulated environment, gradually improving its performance through reinforcement learning.

## **Agentic AI Agent**

It involves a combination of **AI agents** for gathering financial data, analyzing stock performance, and making recommendations.  **Web Search Agent** and the **Finance AI Agent** work together to provide insightful information for making financial decisions, without requiring explicit strategy programming. 

---

- **Web Search Agent**:
  - Uses **DuckDuckGo** as a search tool to fetch relevant information from the web.
  - The agent’s instructions are to always include sources and present the information in a structured markdown format.

```python
web_search_agent = Agent(
    name="Web Search Agent",
    role="Search the web for the information",
    model=Groq(id="llama3-groq-70b-8192-tool-use-preview"),
    tools=[DuckDuckGo()],
    instructions=["Always include sources"],
    show_tools_calls=True,
    markdown=True,
)
```

- **Finance AI Agent**:
  - Uses **Yahoo Finance Tools** to retrieve real-time stock prices, analyst recommendations, stock fundamentals, and news.
  - The agent is set to return data in tables for clarity and ease of interpretation.

```python
finance_agent = Agent(
    name="Finance AI Agent",
    model=Groq(id="llama3-groq-70b-8192-tool-use-preview"),
    tools=[YFinanceTools(stock_price=True, analyst_recommendations=True, stock_fundamentals=True, company_news=True)],
    instructions=["Use tables to display the data"],
    show_tool_calls=True,
    markdown=True,
)
```

- **Multi-Agent System**: Combines the Web Search and Finance AI agents into one team. The team can execute queries together, and the results are returned in a structured, readable format. The agents are instructed to always include sources and present information in markdown format.

```python
multi_ai_agent = Agent(
    team=[web_search_agent, finance_agent],
    instructions=["Always include sources", "Use table to display the data"],
    show_tool_calls=True,
    markdown=True,
)
```

---

#### **3. Query Execution and Information Retrieval**

Once the agents are set up, they can be prompted with specific tasks. For example, to gather stock information for a particular company, you can prompt the multi-agent system to:

- **Search the Web**: The Web Search Agent searches the internet for articles, news, and other relevant content about the company.
- **Retrieve Financial Data**: The Finance AI Agent retrieves stock-related data from Yahoo Finance, such as current stock price, analyst recommendations, fundamentals, and company news.

prompt:
```python
multi_ai_agent.print_response("Provide a stock analysis for Apple Inc. (AAPL) including current price trends and recent market news", stream=True)
```

- Provide an **analysis of Apple Inc. (AAPL)**, including **current price trends**.
- Share **recent market news** related to Apple.

This approach removes the need for manually deciding strategies, as the agents autonomously gather, process, and present the data required for smart financial decisions.

## Create a Conda Environment

```bash
conda create -p <env_name> python=3.10 -y
```

## Activate Your Conda Environment

```bash
conda activate <env_path>
```

- If activating on bash terminal use this command:

```bash
source activate ./<env_name>
```

- Else, use:

```bash
conda activate <env_path>
```

## Install Dependencies from `requirements.txt`

```bash
pip install -r requirements.txt
```

## Create a `.env` File to Store Your Environment Variables

```env
OPENAI_API_KEY=""
PHI_API_KEY=""
GROQ_API_KEY=""

```
