
## 2.  Agent Behaviour / Types
**2a.** False, an agent just has to act as best it can
**2b.** False, same as before
**2c.** True? There could be an environment where all actions have a positive impact on the performance measure.
**2d.** False, a greedy agent like this could conceivably get stuck because of attempting to make the 'most beneficial' move each turn without considering making immediately detrimental choices for long-term benefit.
**2e.** False, the programmer could provide the agent with an algorithm that makes poor decisions based on its 'built-in' knowledge. 

## 3. Tabulation
**3a.** No (although I initially thought we could use conditions or 'buckets' to group inputs in discrete buckets)
**3b.** There are $|P|^T$ possible percept sequences
**3c.** No, it can become incredibly space inefficient


## 4. Environment Properties
**4a.** (semi?)-static, Sequential, Observable, Multi-agent, discrete, deterministic
**4b.** Dynamic, Sequential, Observable, Multi-agent, continuous, deterministic
**4c.** (semi?)-static, episodic, observable, single-agent, discrete, (semi?)-deterministic
**4d.** dynamic, episodic, observable, multi-agent, continuous, (semi?)-deterministic

## 5. Agent Architectures
**5a.** Model-based reflex agent
**5b.** Goal-based agent
**5c.** Reflex agent
**5d.** Utility-based agent
**5e.** Utility-based agent


## 6. Agent Programs / Functions
**6a.** 
**6b.** This depends not only on the environment (i.e. static vs dynamic), but also the starting complexity of the agent program. In a dynamic environment this could allow for incremental improvements that wouldn't be feasible with the slower machine. 

## 7.  Non-determinism
**7a.** The agent program could consider this through repeated observations of the square before and after vacuuming. With enough observations, the 10% faulty observation rate and the 25% vacuum failure rate are outweighed by ensuring we truly know the state of the floor before making any action.
**7b.** Yes, by changing sides to 'observe' constantly (provided there is no penalty for movement).


