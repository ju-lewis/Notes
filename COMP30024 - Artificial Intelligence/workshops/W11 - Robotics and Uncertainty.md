
# 1. Robotics

Let O be an RV indicating whether there is an obstacle or not
Let S be the state of the sensor reading = {fp,fn,tp,tn}

Let P be the event of the sensor producing a positive reading = P(fp) + P(tp)

P(O=1) = 0.1
P(S=fp) = 0.3
P(S=fn) = 0.3



**1a.** 
We can decompose $P(O=1|P,P,P)$ using Bayes' Rule
$$P(O=1 | P,P,P) = \frac{P(P,P,P|O=1)P(O=1)}{P(P,P,P)}$$ 
$$P(O=1|P,P,P) = \frac{P(P,P,P|O=1)P(O=1)}{P(P,P,P|O=1)P(O=1)+P(P,P,P|O=0)P(O=0)}$$
$$P(O=1|P,P,P)=\frac{(1-P(S=fn))^3\times0.1}{(1-P(S-fn))^3\times0.1+P(S=fp)^3\times0.9}$$
$$P(O=1|P,P,P)=\frac{0.7^3 \times 0.1}{0.7^3\times0.1 + 0.3^3\times0.9}$$
$P(O=1|P,P,P)=\frac{343}{586}$



**1b.**
We can decompose $P(O=0|P,P,N)$ using Bayes' Theorem

$$P(O=0|P,P,N)=\frac{P(P,P,N|O=0)P(O=0)}{P(P,P,N)}$$
$$P(O=0|P,P,N)=\frac{P(P,P,N|O=0)P(O=0)}{P(P,P,N|O=0)P(O=0) + P(P,P,N|O=1)P(O=1)}$$

$$P(O=0|P,P,N)=\frac{P(S=tn)P(S=fp)^2P(O=0)}{P(S=tn)P(S=fp)^2P(O=0) + P(S=fn)P(S=tp)^2P(O=1)}$$

$$P(O=0|P,P,N)=\frac{0.7\times0.3^2\times0.9}{0.7\times0.3^2\times0.9+0.3\times0.7^2\times0.1}$$
$P(O=0|P,P,N)=\frac{27}{34}$


