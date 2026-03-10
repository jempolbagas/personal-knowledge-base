---
title:
  - Intelligent Agent
type: Concept
course:
  - Artificial Intelligence
topic:
  - Foundations of AI
semester: 4
tags:
  - artificial-intelligence
  - intelligent-agent
  - rational-agent
  - agent-architecture
created: 2026-03-04
---

# Intelligent Agent

> An autonomous entity that perceives its environment through sensors, and then acts upon that environment through actuators to achieve specific goals — in other words, "something that perceives and acts."

---

## Explanation

In AI classes, we often hear the term **AI = machines that can think**. However, modern approaches (like in Russell & Norvig's textbook) prefer to define AI as **the study and design of Intelligent Agents**. So, whatever the AI system is—ranging from an AC thermostat, an NPC in a game, to Tesla's Autopilot—everything can be viewed as an *Agent*.

Simply put, every agent operates through a basic cycle involving key components and concepts:
1. **Sensor**: A device to **perceive** the environment (e.g., cameras, microphones, text inputs). The input captured at a given moment is a **Percept**, and the history of all inputs is the **Percept Sequence**.
2. **Actuator**: A device to **act** on the environment (e.g., motors, screens, sending a reply). The output produced is the **Action**.
3. **Agent Function & Program**: The **Agent Function** is the abstract mathematical mapping from a percept sequence to an action ($f: \mathcal{P}^* \rightarrow \mathcal{A}$). The **Agent Program** is the concrete implementation of this function running on a specific **Architecture** ($\text{Agent} = \text{Architecture} + \text{Program}$). 

**What is the difference between a regular Agent and an *Intelligent* Agent?**
While simple agents just react, **Intelligent Agents** possess more advanced characteristics:
- **Autonomous**: Acting independently, guided by their own experience rather than just built-in knowledge.
- **Reactive & Proactive**: Responding quickly to changes while also taking initiative (goal-directed behavior).
- **Flexible & Robust**: Having multiple ways to reach a goal and recovering from failures.
- **Social & Situated**: Able to communicate with other agents/humans and exist within a specific environment.
- **Learning**: Able to improve performance over time through experience.

In AI, we also heavily focus on building **Rational Agents**. A rational agent is an agent that always strives to **maximize its performance measure**, based on the information (perceptions) it receives and the knowledge it possesses. Keep in mind, **rational doesn't mean omniscient or perfect**, but rather *taking the best possible action based on the available information at that moment*.

**5 Types of Agents (from the most basic to the smartest):**
1. **Simple reflex agent**: Only executes basic *If-Then* rules. (Ex: "If distance ahead < 1 meter → Brake!").
2. **Model-based reflex agent**: Has an internal "memory" about the current state of the world, so it knows a bit about things not directly visible to sensors.
3. **Goal-based agent**: Has a *goal* to achieve, so it thinks ahead: "Which action will bring me closer to my goal?"
4. **Utility-based agent**: Doesn't just chase a goal, but also cares about *quality*. If there are many ways to reach the goal, it chooses the most "profitable" or efficient way.
5. **Learning agent**: An agent that might not be very smart initially, but can learn from *feedback* and past experiences to become better over time.

**Types of Environments:**
An agent's world (the **Task Environment**) can be very simple or incredibly complex. We usually classify them based on several properties:
- **Fully Observable vs. Partially Observable**: Can the agent's sensors see the *entire* state of the environment at all times? (Chess board = Fully; Poker game or Driving = Partially).
- **Deterministic vs. Stochastic**: If the agent performs an action, is the resulting state 100% guaranteed? (Tic-Tac-Toe = Deterministic; Driving = Stochastic). *Note: If a deterministic environment is only unpredictable due to the actions of other agents, it is called **Strategic**.*
- **Episodic vs. Sequential**: Is the agent's life divided into separate, independent "episodes" where past actions don't affect future ones? (Image classification = Episodic; Playing Chess = Sequential).
- **Static vs. Dynamic**: Does the environment change while the agent is thinking? (Crossword puzzle = Static; Driving = Dynamic). *Note: If the environment doesn't change but the agent's performance score does (e.g., losing points for time spent thinking), it is **Semidynamic**.*
- **Discrete vs. Continuous**: Is there a limited, countable number of states and actions, or a smooth/infinite range? (Chess = Discrete; Driving = Continuous speed and steering).
- **Single-agent vs. Multi-agent**: Is the agent alone, or are there other agents it needs to cooperate with or compete against? (Solving a Sudoku = Single; Pac-Man = Multi-agent).

---

## Analogy / Intuition

When designing an agent, we define its **Task Environment** using the **PEAS** framework: **P**erformance measure, **E**nvironment, **A**ctuators, and **S**ensors.

Just imagine an **Online Taxi (Ride-hailing) driver**. The PEAS formulation would be:
- **Performance:** Fast arrival, passenger comfort, no traffic violations, save fuel.
- **Environment:** Roads, other cars, pedestrians, weather, traffic lights.
- **Actuators:** Hands and feet to steer, accelerate, brake, honk, use signals.
- **Sensors:** Eyes to see the road, speedometer, and phone screen/GPS.

A *rational* driver is one who always tries to maximize their *performance measure*. When they see the GPS showing a green road, they choose to go through it. If it turns out there's suddenly a fallen tree ahead that wasn't on the GPS, they are still considered rational when they took that route, because at the time of the decision, that route was the best choice based on their percept sequence and the knowledge they had.

To make complex decisions, agents might use a **BDI (Belief-Desire-Intention)** architecture:
- **Belief**: The agent's knowledge about the environment (e.g., "The road ahead is closed due to a fallen tree").
- **Desire**: The agent's goals (e.g., "Reach the destination quickly").
- **Intention**: The specific plan of action chosen to achieve the desire (e.g., "Take the highway detour route").

---

## Concrete Example

The classic textbook example is usually the **Robot Vacuum Cleaner (Roomba)**:

- **P**erformance Measure: The floor is as clean as possible, battery is conserved, and the job doesn't take too long.
- **E**nvironment: The room's floor, furniture layout, and dirt spots.
- **A**ctuators: Wheels to move around, vacuum motors to suck up dirt.
- **S**ensors: Infrared sensors, dirt sensors, bump sensors.

Initially, this robot might just be a **simple reflex agent** (The moment it bumps a chair → reverse and turn). But more advanced robots can level up to be **model-based** (saving a digital map of the clean room) or a **learning agent** (learning the homeowner's schedule so it can vacuum when the house is empty).

---

## Connections

- **Part of:** [[Foundations of AI]], [[Konsep Kecerdasan Buatan]]
- **Relates to:** [[Rational Agent]], [[Agent Environment]], [[Machine Learning]], [[Search Algorithms]]
- **Used in:** [[Robotics]], [[Game AI]], [[Autonomous Vehicles]], [[Expert System]]
- **Contrasts with / Don't confuse with:** "AI" in general — Intelligent Agent is the *formal framework* for defining AI, not a synonym. Also, don't confuse it with just chatbots or virtual assistants — they are merely *one implementation* of an intelligent agent.

---

## Open Questions

- How do you determine the right *performance measure* for an agent? Who defines it — the designer or the agent itself?
- Is it possible for a perfectly rational agent to make a choice that is morally wrong — and if so, does that mean rationality alone is not enough?
- In the context of the course, what exactly is the relationship between the types of agents (simple reflex, model-based, etc.) and the algorithms we'll learn (BFS, DFS, A*, Decision Tree, ANN)?

---

## Sources

- Originated from: [[Konsep Kecerdasan Buatan - AI - 2]], [[Intelligent Agent - AI - 3]]
- Reference: Russell, S. & Norvig, P. — *Artificial Intelligence: A Modern Approach*, 3rd Ed. — Chapter 2: Intelligent Agents
- Reference: Suyanto — *Artificial Intelligence: Searching, Reasoning, Planning and Learning*, 2007
- External: [IBM — AI Agents](https://www.ibm.com/think/topics/ai-agents)
- External: [Wikipedia — Intelligent Agent](https://en.wikipedia.org/wiki/Intelligent_agent)
- External: [GeeksForGeeks — Agents in AI](https://www.geeksforgeeks.org/agents-artificial-intelligence/)
