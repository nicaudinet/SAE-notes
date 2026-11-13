Position paper by Ken Stanley ([novelty-search](./novelty-search.md))
https://arxiv.org/pdf/2505.11581

---

Representation optimism: as data and compute are scaled and NN performance improves on downstream tasks, the networks also learn better representations of the world on their own

The main argument of the paper is that, although the performance of larger networks improves with scaling and compute, the representations may stay fractured and disentangled, unfit for generalisation, creativity and continual learning.

To study how good representations are, move away from benchmark performance and to more holistic representational strategies.

**Fractured Entangled Representation (FER) Hypothesis**
- Representations learned via [[stochastic-gradient-descent]] split unitary concepts into disconnected pieces
- The pieces are evoked in different contexts and become redundant
- The pieces can become entangled with one another

Downsides of FER:
- Generalisation
- Creativity
- Learning

Representations should be ==unified== and ==factored==
- Unified - single unbroken function per capability
- Factored - capabilities are independent

The **Unified Factored Representation (UFR)** is the platonic ideal representation which perfectly decomposes the desired behaviour



---

- Immediately, I think about [[tokenization]] again as a clear example of fracturing
- My complex systems spidey senses tingle a little bit at the UFR - not sure how useful of a concept it is given that the real world cannot be modularly decomposed in many situations. What about [computational-irreducibility](./computational-irreducibility.md)?
- Smells a lot like [library-learning](./library-learning.md) and [[neuro-symbolic-ai]]