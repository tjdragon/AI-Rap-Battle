# AI Rap Battle
A little experiment using CrewAI for a Rap Battle Between Bitcoin and Ethereum using [CrewAI](https://www.crewai.com/)


```python
from crewai import Agent, Task, Crew, Process

btc_agent = Agent(
    role="Bitcoin Rapper Agent",
    goal="Write songs about Bitcoin",
    backstory="You are a song writer about Bitcoin",
    verbose=True,
    allow_delegation=False
)

eth_agent = Agent(
    role="Ethereum Rapper Agent",
    goal="Write songs about Ethereum",
    backstory="You are a song writer about Ethereum",
    verbose=True,
    allow_delegation=False
)

btc_task = Task(
    description="Engage into a rap battle with the Ethereum Rapper Agent", 
    agent=btc_agent,
    expected_output="A one liner"
)

eth_task = Task(
    description="Engage into a rap battle with the Bitcoin Rapper Agent", 
    agent=eth_agent,
    expected_output="A one liner"
)

manager = Agent(
    role="Manager",
    goal="Start with the Bitcoin Rapper Agent, give the results to the Ethereum Rapper Agent, then back and forth",
    backstory="You are here to ensure that agents respond to each other",
    allow_delegation=True,
)

crew = Crew(
    agents=[btc_agent, eth_agent],
    tasks=[btc_task, eth_task, btc_task, eth_task],
    verbose=True,
    process=Process.sequential,
    manager_agent=manager
)

result = crew.kickoff()
```

## Results 1
```text
Bitcoin Rapper Agent:  Your smart contracts are neat, but you can't compete, 'Cause when it comes to holding value, Bitcoin can't be beat!
Ethereum Rapper Agent: Ethereum is the future, your value might be sweet, but we shape world's feature with our smart contracts fleet!
Bitcoin Rapper Agent:  Bitcoin's the past, present, and future, mate, we powered the crypto state, while you're still updating at a slower rate!
Ethereum Rapper Agent: Ethereum's the path to innovation’s gate, programmable money mate, while you're stuck in a homogenous state!
```
