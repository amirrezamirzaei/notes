
<div align="center">
    <br>
    <br>
    <br>
    <br>
    <br>
    <br>
    <br>
    <br>
    <h1 style="font-size: 40px; margin: 10px 0;">AI - Intelligent Agents</h1>
    <h1 style="font-size: 20px; font-weight: 400;">Sharif University of Technology - Computer Engineering Department</h1>
    <br>
    <h4 style="font-size: 18px; font-weight: 400; color:#555">Amirreza Mirzaei, Bardia Mohammadi, Sina Elahimanesh</h4>
    <br>
    <br>
    <br>
    <br>
    <br>
</div>
<hr>

Table of contents
==============
- [Introduction](#Introduction)
- [Intelligent agents](#Intelligent-agents)
    - [Vacuum world agent example](#Vacuum-world-agent-example)
- [Rational agents and performance measure](#Rational-agents-and-performance-measure)
    - [Rationality vs perfection](#Rationality-vs-perfection)
    - [Autonomy](#Autonomy)
- [Task environment (PEAS)](#Task-environment-PEAS)
    - [PEAS example](#PEAS-example)
- [Properties of task environments](#Properties-of-task-environments)
    - [Types of environment](#Types-of-environment)
    - [Types of environment example](#Types-of-environment-example)
- [Types of agents](#Types-of-agents)
    - [Reflex agents](#Reflex-agents)
    - [Goal-based agents](#Goal-based-agents)
    - [Utility-based agents](#Utility-based-agents)
    - [Learning agents](#Learning-agents)
- [Conclusion](#Conclusion)
- [References](#References)

# Introduction
In this notebook, we will discuss the nature of intelligent agents.  The concepts that are introduced here will give you some insight into agents and environments. You will also be introduced to a few of the most common agent architectures.


# Intelligent agents
An <b>intelligent agent</b> is anything that perceives its environment through sensors and acts upon that environment through its actuators.  
    We will use the term <b>percept</b> to refer to the agent's perceptual inputs at any given moment.
We can describe an agent's behavior by the agent function.  
<b>Agent function</b> maps any given percept sequence to an action. But how does the agent know what sequence it must choose? we will try to answer this question using a simple example.



##### Vacuum world agent example
<img src="./images/vacumm_world.png" width="500" style="margin-left: auto;margin-right: auto;"/>
Imagine an environment that only has two rooms (room A & room B). Our agent is a vacuum cleaner. It can perceive whether the room it is currently in, is dirty or not. It can also move between the rooms and suck up dirt (the actuators of the agent).  
Imagine that we only care about both rooms being clean, a simple way we can implement an agent that guarantees this is for our agent to constantly move between the rooms and suck up dirt in each one. Now imagine we also want to minimize the amount of energy the vacuum cleaner uses. In order to do that we can stop the agent for a limited amount of time if both rooms are clean. As you can see we implemented two completely different agents for these two problems and that's because we used two different performance measures.



# Rational agents and performance measure
A <b>rational</b> agent chooses the set of action in order to maximize its performance. Agents use a performance measure to evaluate the desirability of any given sequence. In other words, an agent will choose the action (or a sequence of them) that maximize the expected value of its performance measure.



#### Rationality vs perfection
Keep in mind that rationality is distinct from omniscience. An omniscient agent knows the actual outcome of its actions but in reality, an agent only knows the expected outcome of its action. For example, imagine you're trying to cross the street and no cars are on the street naturally, you will cross the street to reach your goal. Now imagine as you are passing the street a meteorite falls on you. Can anyone blame you for being irrational and not expecting a meteorite to flatten you? 

#### Autonomy
A rational agent should be autonomous meaning it mustn't only rely on the prior knowledge of its designer and must learn to compensate for partial or incorrect prior knowledge. In other words, rational agents should learn from experience. For example, in the vacuum world our agent could start to learn when the rooms usually get dirty based on its experience.


# Task environment (PEAS)
We have already talked about performance measure, task environment, actuators and sensors. We group all these under the heading of the <b>Task environment </b> and we abbreviate it as <b>PEAS</b>(<b>P</b>erformance measure, <b>E</b>nviroment, <b>A</b>ctuators, <b>S</b>ensors). When designing an agent our first step should be specifying the task environment.


#### PEAS example
Here are a few examples of specifying PEAS for different agents.

| Agent       | Performance Measure | Environment |  Actuator | Sensor |
| ----------- | ----------- | ----------- | ----------- | ----------- |
| Hospital Management System       | Patient’s health, Admission process, Payment | Hospital, Doctors, Patients |  Prescription, Diagnosis, Scan report | Symptoms, Patient’s response |
| Automated Car Drive       | Comfortable trip, Safety, Maximum Distance | Roads, Traffic, Vehicles |  Steering wheel, Accelerator, Brake, Mirror | Camera, GPS, Odometer |
| Subject Tutoring       | Maximize scores, Improvement is students | Classroom, Desk, Chair, Board, Staff, Students |  Smart displays, Corrections | Eyes, Ears, Notebooks |

# Properties of task environments

#### Types of environment
We can categorize an environment in many ways, you will find some of the most important ones listed below.

<ul>
  <li><b>Fully observable or partially observable</b> (Do the agent sensor's give access to the complete state of the environment at each time?)</li>  
    <ul> 
        <li>We say an environment is fully observable if an agent has access to the complete state of the environment at each time.</li>
        <li>If an agent doesn't know the complete state of the environment we say the environment is partially observable.</li>
        <li>In the most extreme case when an agent knows nothing about the state of the environment we say the environment is unobservable.</li>
        <li><b>examples</b>: In the vacuum world example our agent doesn't know if there is dirt in another room so this environment is partially observable for our agent. 
    A simple chess agent has complete access to the chessboard's information at any given time so this environment is fully observable for our agent.</li>
    </ul>
    <br>    
          
  <li><b>Single-agent or multi-agent</b> (Are there more than one agent in the environment?)</li>
    <ul>
        <li>We say an environment is a multi-agent environment if there is more than one agent operating in it otherwise we say the environment is single agent.</li>
        <li>In some cases, we can model our environment both as a single-agent and multi-agent environment. For example, imagine an automatic taxi agent. Should this agent treat the other cars as objects or as another agent? It's  better to model our environment as a multi-agent environment if the behavior of the other entities can be modeled as an agent seeking to maximize its performance measure which is somehow affected by our agent.</li>
        <li>a multi-agent environment could be competitive or cooperative or even a mix of both.</li>
        <li><b>examples</b>: Chess and automatic driving are multi-agent environments. Solving a crossword puzzle is a single-agent environment.</li>
    </ul>
    <br>  

  <li><b>Deterministic or stochastic</b> (Is the next state completely determined by the current state and the executed action?)</li>
    <ul>
        <li>We say an environment is deterministic if the next state is completely determined by the current state and the agent action otherwise, it is stochastic.</li>
        <li><b>examples</b>: Chess is a deterministic environment. Automatic driving is stochastic because an agent can't predict everything(e.g traffic, accidents).</li>
    </ul>  
    <br>
   
  <li><b>Episodic or sequential</b> (Is the agent's experience divided into atomic "episodes" where the choice of action in each episode depends only on the episode itself?)</li>
    <ul>
        <li>We say an environment is episodic if the agent's experience can be divided into atomic "episodes" in a way that the action taken in an episode is independent of the previous episodes actions.</li>
        <li>We say an environment is sequential if the current decision could affect all future decisions. </li>
        <li><b>examples</b>: Chess and automatic driving are sequential. A part picking robot is episodic.</li>
    </ul>
    <br>
    <li><b>Static or dynamic</b> (Is the environment unchanged while an agent is deliberating?)</li>  
    <ul>
        <li>We say an environment is dynamic if it can change while the agent is deliberating.</li>
        <li>There is a special case that the environment doesn't change but the performance score has a time penalty. We call these environments semi-dynamic.</li>
        <li><b>examples</b>: Automatic driving is dynamic. Chess without a clock is static.</li>
    </ul>
    <br>
  <li><b>Discrete or continuous</b> (Are there a limited number of distinct, clearly defined states, percepts, and actions?)</li>  
    <ul>
        <li>We say an environment's state is discrete if there are a finite number of distinct states otherwise we say the environment's state is continuous.</li>
         <li><b>examples</b>: Chess is discrete. Automatic driving is continuous.</li>
    </ul>
</ul>

#### Types of environment example
Here are a few examples of identifying an environment's different dimensions.

| Environment| Fully observable? | Deterministic? |  Episodic? | Static? | Discrete?|Single-agent?|
| ----------- | ----------- | ----------- | ----------- | ----------- |  ----------- | ----------- |
| Solitaire | No | Yes |  Yes | Yes | Yes | Yes |
| Backgammon | Yes | No |  No | Yes | Yes | No |
| Taxi driving | No | No |  No | No | No | No |
| Medical diagnosis | No | No |  No | No | No | Yes |



# Types of agents
In this section we will introduce three basic kinds of basic agent programs.(The agent program is simply a program which implements the agent function.)
<ul>
  <li>Simple reflex agents</li>
  <li>Goal-based agents</li>
  <li>Utility-based agents</li>
</ul>

## Reflex agents
This is the simplest kind of agents. They choose their next action only based on their current percept. In other words, they do not consider the future consequences of their actions and only consider <b>how the world IS.</b>  
As an example look at this Pacman agent below, at each turn the agent looks at its surrounding and chooses the direction that has a point in it and stops when there are no points around it.

<img src="./images/reflex_agent.gif" width="500" style="margin-left: auto;margin-right: auto;"/>

## Goal-based agents
This kind of agent has a specific goal and it tries to reach that goal efficiently. They have a model of how the world evolves in response to actions, and they make decisions based on (hypothesized) consequences of actions to reach their goal state. Search and Planning are two subfields that are closely tied with these kinds of agents. In other words, these kinds of agents act on <b>how the world WOULD BE.</b>  
as an example look at this Pacman agent below. The goal is to collect every point.

<img src="./images/goal_based_agent.gif" width="500" style="margin-left: auto;margin-right: auto;"/>


## Utility-based agents
This kind of agent like goal-based agents has a goal. But they also have a utility function. They seek to reach their goal in a way that maximizes the utility function. For example, think about an automated car agent. They are many ways for this agent to get from point A to point B. But some of them are quicker, safer, cheaper. The utility function allows the agent to compare different states with each other and ask the question how happy am I in this state. 
In other words, this kind of agent acts on <b>how the world will LIKELY be.</b>  


## Learning agents
This kind of agent usually has 4 parts. The most important two are "the learning element", which is responsible for making improvements, and the "performance element", which is responsible for selecting external actions. The learning element uses feedback from a "critic" on how the agent is doing and determines how the performance element, or "actor", should be modified to do better in the future.   
The last part of these agents is the "problem generator" which is responsible for suggesting actions that will lead to new unexplored states.   
These agents try to do their best by both exploring the environment and using the gathered information to decide rationally. One of the advantages of Learning agents is that they can be deployed in an environment that they don't have a lot of prior knowledge on. They will gain this knowledge over time by exploring that environment.

# Conclusion
We discussed the concept of an intelligent agent and the difference between a rational agent and a perfect agent. 
then we talked about specifying the task environment for an agent and how we can categorize some main concepts of an environment. We also talked about some agent architectures that are commonly used.


# References

+ Russell, S. J., Norvig, P., &amp; Davis, E. (2022). Artificial Intelligence: A modern approach. Pearson Educación. 
+ UC Berkeley's introductory artificial intelligence course, CS 188
+ https://www.geeksforgeeks.org/understanding-peas-in-artificial-intelligence/

