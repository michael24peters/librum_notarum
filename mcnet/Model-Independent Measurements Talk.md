---
tags:
  - lecture/mcnet
  - mcnet
date: 2024-06-10
---

![[model_indep_measurements_2024_06_10.pdf]]

- Measure higgs width (4 MeV) impossible due to its mass width in comparison to detector resolution (10 GeV)
- Connect number of events (what I measure) to cross section (what I want to measure)
	- Experimental: 
		- Calibrate (detector measures voltage; want useful energy (GeV))
		- Finite resolution: measure something at 1000 GeV, has uncertainty at each of these kinds of points
		- Some places aren’t being covered (beam pipe, etc.)
		- Detector not perfectly efficient
	- Theoretical:
		- Cut pre- or post-hadronization
		- Final state particle definition (lifetime cut, e.g. ≥10 ps lifetime)
	- We use MC + simulation. 
		- Can start with theory, run detector simulation, then predict number of events to expect. Compare with data we collect. In other words, physics to number of events
		- Take data, undo detector effects (see Experimental above), i.e. unfolding, compare to theory, correct to phase space/particle definition. Choice is analysis-specific. In other words, number of events back to physics.
- Not sure what was done to reduce uncertainty/what MC is being “constrained” by to cause such a significant reduction in uncertainty. Answer (kinda): reweighting the MC based on the data. We should only do that for things we expect the MC to be poor at doing, e.g. Z production from electroweak dominated by Z production, so if we try to model Z electroweak it will not turn out well, so we need to do this constraining to reduce this uncertainty. Hmm. (Use Mjj to constrain/control)
- [ ] #mcnet What does “on-shell” mean?
- 