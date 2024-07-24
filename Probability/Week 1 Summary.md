
## Experiments, Outcome Spaces, and Events

A **random experiment** is a process which has *(potentially infinite)* possible outcomes.
- Examples:
	- Tossing a coin
	- Rolling a die
	- A horse race

An **outcome space** or **sample space** ( $\Omega$ ) is the set of *all* possible outcomes. i.e. it describes the results of the random experiment.
- Examples:
	- Coin toss: $\Omega = \{H, T\}$
	- Rolling a die: $\Omega = \{1,2,3,4,5,6\}$
	- Horse Race: $\Omega = \{\text{all horses in the race}\}$

An **event** is a set of possible outcomes within the sample space of an experiment. So $\text{Event } A \subset \Omega$ . Event A occurs if the observed outcome $\omega \in A$
- Examples:
	- Flipping a heads: $A = \{H\}$
	- Rolling an even number: $A = \{2,4,6\}$

$\Omega$ is known as the *certain event* as all outcomes are within the outcome space.
$\emptyset$ is known as the *impossible event* since it contains no outcomes.

### Set Operations on Events
$A \cup B$ is the *event* that $A$ or $B$ occur.
$A \cap B$ is the *event* that both $A$ and $B$ occur.
$A^c$ is the *event* that $A$ does not occur.

$\omega \in A$ means the outcome $\omega$  is in the event $A$.

If $A$ is *finite*, which is not very common, $\#A$ refers to the number of elements in $A$.

If $A \cap B = \emptyset$ then $A$ and $B$ are *disjoint* or *mutually exclusive*.
If $A \cup B = \Omega$ then $A$ and $B$ are *exhaustive*.

#### Example:
Prove $B$ is *impossible* if and only if for every event $A$:
$$A = (B \cap A^c) \cup (B^c \cap A)$$
##### Case 1 - $A$ Occurs:
$\text{If }A\text{ then either } (B \cap A^c)\text{ or }(B^c \cap A)$ occur.
As $A$, $(B \cap A^c)$ does *not* occur, so $(B^c \cap A)$ must occur, which implies that $B$ does *not* occur.

##### Case 2 - $A$ Does *not* occur:
If $A^c$ then *neither* $(B \cap A^c)$ or $(B^c \cap A)$ can occur.
For $(B \cap A^c)$ to *not* occur when $A^c$, then $B$ can't occur.

Hence when $A$, $B$ doesn't occur and when $A^c$, $B$ doesn't occur.
Thus, $B$ is impossible.



