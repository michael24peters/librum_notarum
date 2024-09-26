---
tags:
  - fleeting
created: 2024-08-14 10:00
date: 2024-08-14
moc:
  - "[[Commissioning tests]]"
  - "[[Codex hardware]]"
---
# 202408140959 Issues with automating commissioning tests

I'm not convinced I can *fully* automate this process. Having gone through and been reminded of the many different outputs, the variety and complexity of "bad collections" is beyond what can be filtered by software. The TDCs are just very unpredictable in the misbehavior. I also forgot that you have to manually change the triggers every run.

The maximum amount of automation that can be done is 13 successful runs at a time. After that, I have to switch the cables on the trigger board manually.

## Potential solution(s)

- **Ethernet and switch for CAEN power supply** to control everything from my computer. *Good idea, no downsides.*
- **Throw out *obviously* bad runs**, e.g. missing layers in data acquisition. *Marginal gain; would still require constant attention.*
- ***Attempt* to automate**, then manually look at plots and re-run as needed. *Better, but still requires attention and doubling back*.
- Filters need to be made by relative difference between the two trigger layers and min-max cuts on every layer, as demonstrated below. *This is near-impossible for the test layer.* Alternatively, you could just check the trigger layers (with obvious drawbacks).

## Examples

Not that I need to do this, but as evidence that this is a TDC, here's a chamber noise test (all layers at working point, trigger off, i.e. taking in everything). What you find is that the bottom layer in its entirety is not detected, which obviously makes no sense.

![[eff-scan-0.png]]

(I copied the run to my clipboard, overwrote the run, then stupidly copied something else) You would have do a percent difference from the other layer to make this one work. Sometimes the hits are both at 400, or both at 600. Taking the mean or median here would have made them both land in the tolerance range, even though there was clearly an issue. 

![[Bad run example at 4.8kV]]

This is an efficiency scan for the bottom layer. This can be automated away. A simple comparisons of average or relative difference would work.

![[eff-scan-1.png]]

This is an obviously bad run, but by averages or percent difference it would actually be fine for a top layer efficiency scan (unless you set a max on a single channel's possible hit count). Cuts could catch this error.

![[eff-scan-2.png]]

(No example yet) There are times where one or two channels are drastically too large, but the average, median, and relative difference would still be within the tolerance range. This is a bad run and should usually be tested again. 

At the same, there are times when a group of channels have more hits than the other channels of its layer and it's not an issue. For example, look at the following plot:

![[eff-scan-4.png]]

This is a strange one for testing the middle layer at 6000 V, where the results are technically correct but the amount of mid hits is suspiciously high.

![[eff-scan-5.png]]

---
# References


