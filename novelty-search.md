Novelty search is the idea of exploring a search space by constantly trying to find new and interesting behaviours. Importantly, this process is _not_ driven by objectives. The only criteria for considering something "good" is how novel it is compared to what's already been done. In the language used in [why-greatness-cannot-be-planned](./why-greatness-cannot-be-planned.md), this process is a stepping-stone collector.

Novelty search is in some sense "true exploration" in the [[explore-extract]] tradeoff. It is exploration without judgement or bounds. An objective is a judgement of how useful something is towards a particular goal.

Novelty search relies on the ability to differentiate what is different and novel from what has already been done. This relies on two forms of intelligence:
- Memorisation: knowing what has already been done
- Computation: being able to compare the new with the old

Example domain: robot trying to learn how to exit a corridor.