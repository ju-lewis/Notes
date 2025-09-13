
Regular expression are a compact notation for describing regular languages.


## Formal Syntax

For an alphabet $\Sigma = \{a_1,...,a_n\}$:
$$regexp \to a_1 | \  ... \ | \ a_n \ | \ \epsilon \ | \ \emptyset \ | \ regexp \cup regexp \ | \ regexp \circ regexp \ | \ regexp*$$

**Semantics:**
(Languages described by a given regular expression)

$L(a) = \{a\}$
$L(\epsilon) = \{\epsilon\}$
$L(\emptyset) = \emptyset$
$L(R_1 \cup R_2) = L(R_1) \cup L(R_2)$
$L(R_1 R_2) = L(R_1) \circ L(R_2)$
- *Note:* we often omit the concatenation operator
$L(R*) = L(R)*$

>[!Info] Binding Precedence
>Star > Concatenation > Union

## Translation

### From Regular Expression to NFA

>[!Example] Theorem
>A language is regular if and only if it can be expressed as a regular expression.

Use translation rules discussed in [[L13 - NFAs]]

### From NFA to Regular Expression
1. Start by making sure the NFA has at most 1 accept state
2. Repeatedly eliminate states that are neither start nor accept states
3. In the process, arcs get labelled with regular expressions

![[nfa-to-regex.png]]

# Limitations of Finite Automata

Cannot look ahead
- Fixed number of bits in memory

How many bits to recognise this, without lookahead?
$$\{0^n1^n | n \geq 0\}$$


