---
tags:
  - analysis
  - question
---
- [ ] #analysis Walk through advance(), stripping line, print(candidates[0]). See halfway down [this](https://lhcb.github.io/starterkit-lessons/first-analysis-steps/interactive-dst.html) page
	- [ ] #question #analysis What did I do/filter out in advance()? See [here](https://lhcb.github.io/starterkit-lessons/first-analysis-steps/interactive-dst.html) 
		- We convert to ntuple to have just the info we want from the DST file.
		- Also see here below
```python
line = 'D2hhPromptDst2D2KKLine'
advance(line)
```
- [ ] #issue #analysis Still can’t run TBrowser with -X or -Y flags. Mention ssh config file you create. See [here](https://lhcb.github.io/starterkit-lessons/first-analysis-steps/minimal-dv-job.html) ⏫
- [ ] #issue #analysis DecayTreeTuple error when I tried to run it. See See [here](https://lhcb.github.io/starterkit-lessons/first-analysis-steps/minimal-dv-job.html) ⏫
- [ ] #question #analysis Why do we need to use LoKi functors? 🔽 
	- I understand that it may automate some tasks, which is very nice, but other times the starter kit just uses it to get x, y, z momentums, masses, etc. Can’t we just use the LHCb::Particle class and access its parameters/variables (either directly if public or through getters if private)
	- So do LoKi functors come into play in stripping lines, trigger lines, and DaVinci options? Starterkit says so, but I suppose I’m curious what form that takes in practice. I don’t fully understand yet what a stripping line would look like and what options or lines I would need of my own analysis in the future, i.e. I lack some context for real use case.
- [ ] #analysis Navigating a tree with LoKi functors (see bottom of [this](https://lhcb.github.io/starterkit-lessons/first-analysis-steps/loki-functors.html) page)

```python
from LoKiPhys.decorators import MAXTREE, ISBASIC, HASTRACK
MAXTREE(ISBASIC & HASTRACK, PT, -1)(candidate) == max_pt
```