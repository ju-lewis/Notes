
# The Agent Model
The rational agent is the basis of "Artificial Intelligence: A Modern Approach"


**Percepts**
- Observations of the environment, made by *sensors*
**Actions**
- Actions may affect the environment, made by *actuators*
**Environment**
- Space in which the agent exists
**Performance Measure**
- Measure of the desirability of environment states


>[!example] 
>## Automated Taxi
>**Percepts**: Video, accelerometers, gauges, engine sensors, GPS, etc.
>**Actions**: Steer, accelerate, brake, horn, display, etc.
>**Environment**: City streets, freeways, traffic, weather, pedestrians, customers
>**Performance Measure**: Safety, profitability, laws obeyed, comfort

# Agents as Functions

Agents can be evaluated empirically, sometimes analysed mathematically
Agent is a function from *percept sequences* to actions

Ideal rational agent would pick actions which are expected to maximise its *performance measure*

>[!note]
>Rational $\neq$ Omniscient
>Rational $\neq$ Clairvoyant
>Rational $\neq$ Successful



# Agent Types

### Simple Reflex Agents

Simple reflex agents take in the state of the environment (through *percepts*), and simply act upon the current state based on predefined rules (i.e. "if this is the state, then perform this action")

![[simple-reflex-agent.png]]

Simple reflex agents *do not have any memory*.

### Model-Based Reflex Agents

Model-based reflex agents infer additional information about the current state of environment (e.g. change over time) that cannot be directly observed with percepts.

![[model-based-reflex-agent.png]]

This agent still operates based on condition-action rules

### Goal-Based Agents

Goal-based agents incorporate the ideas of "thinking ahead" and interpreting the impacts of decisions in relation to goals.

![[goal-based-agent.png]]

An example could be a chess bot that has the goal of checkmating the opponent, moves are decided based on how they progress the state of the environment and agent towards the intended goal.

Goals are a single, specific end-state that the agent wishes to achieve.

### Utility-Based Agents

A utility based agent uses a utility function to determine how 'happy' the agent will be in a given state (as a measure of desirability).

![[utility-based-agent.png]]

The distinction between the utility function and a goal-seeking agent is a utility function is able to describe any state *without an exact goal* in mind.


# Environment Types

**Observable**: Percepts contain all relevant information about the world
**Deterministic**: Current state of the world uniquely determines the next
**Episodic**: Only the current (or recent) percept is relevant, and short-term actions do not have long-term consequences
- *Episodic*: Object classification
- *Sequential*: Chess
**Static**: Environment doesn't change while the agent is deliberating (turn-based)
**Discrete**: Finite number of possible environment states




# Summary
- Characterise requirements for an agent in terms of its percepts, actions, and environment
- Choose and justify agent type for a given problem
- Characterise the environment for a given problem