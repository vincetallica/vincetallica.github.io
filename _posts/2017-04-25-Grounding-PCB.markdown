---
layout: post
title:  "How to reduce EMI on boards with both analog and digital signal by grounding effectively!"
date:   2017-04-25 12:00:00 -0800
categories: Engineering
---

I’ve built various analog and digital PCB design with a team of engineers, and one of the few things that I wish someone taught me in school and that I didn’t have to learn from experience is how to design grounding correctly.  I’ve had designs where the circuit simply didn’t work because one of the digital components had return currents from bad grounding placement.  There are many different ways, and designing PCB requires a logic mind, and a creative one to work with the noise and safety constraints and more often than not, engineers have disagreements on how a PCB should be laid out.  Unfortunately, grounding is one of those topics with no “recipe” approach that guarantees largest reduction in EMI (electromagnetic interference) and if not done correctly can be an issue for analog or digital designs alike. Let’s take a look at some grounding considerations, and proposed solutions to solve your issues on analog, digital or mixed signal design.

## Ground Planes and Ground Points ##

A low inductance ground system is an important element when designing a PCB for minimizing EMC. To do that, you should utilize ground planes (i.e. a layer of copper set as ‘ground’) to maximize the ground area on a PCB. This reduces the inductance of ground in the system, which in turn reduces electromagnetic emissions and crosstalk.

## How to design Grounding Single Layer PCBs ##

Don’t do: In my experience,  I’ve had a good scolding from my technical lead when I tried connecting component’s ground pins randomly to ground points without a plane, because this generates high ground inductance and leads to EMI issues!
Do: Luckily, I was told a full ground plane provides the lowest impedance as the current returns back to its source.
Watch out for this: When I implemented a ground plane and connected individual grounds together before connecting them to the ground plane, I got scolded again, because that not only increases the size of current loop but also increases the probability of ground bouncing, which is again not ideal.   

## Grounding Multilayer PCBs##

PCB usually has 2 or more layers. I suggest you ensure power plane to manage distribution of power lines and ground plane to run over large section of one layer to prevent cross-talk between lines above it on adjacent layer.  If more than two layers are used, then one complete layer should be used as a ground plane. In the case of a four-layer board, the layer below the ground layer should be used as a power plane (see Figure 2a which shows one such arrangement). Care must be taken that the ground layer should always be between high-frequency signal traces and the power plane. If a two-layer board is used and a complete layer of ground is not possible, then ground grids should be used. If a separate power plane is not used, then ground traces should run in parallel with power traces to keep the supply clean.

However, ground planes require a dedicated PCB layer which may not be feasible for multiplayer PCBs, so another way is to use ground grids as shown in Figure 1a where inductance will depend on the spacing between the grids. Also, a signal returns to system ground using via is also very important because when a signal takes a longer path, it creates a ground loop which is a no-no because it forms an antenna and radiates energy.  Hence, every trace carrying current back to the source should follow the shortest path and must go directly to the ground plane (as shown in Figure 1b)!

## Separate Analog and Digital Grounds ##

For Digital Circuits, pay extra attention to traces connecting clocks and other high-speed signals to keep them as short as possible and be adjacent to the ground plane to keep radiation and crosstalk under control.  For just Analog Circuits, traces carrying analog signals should be kept away from high-speed or switching signals and must always be guarded with a ground signal. A low pass filter should always be used to get rid of high-frequency noise coupled from surrounding analog traces.

For mixed signal designs, you’ll hear it all the time, keep analog and digital circuits separate on the PCB! Likewise, for the ground keep the digital ground and analog ground separate and the communication lines between the two partitions can be connected by a small passage. All you need between the two islands of analog and digital is a single point of star ground! That is you can connect the digital ground plane to the power source's ground connection and the analog ground plane to the same physical point. The small passage should be capable of handling any current that could potentially flow through it.


## Use Star Ground ##
In your design I highly recommend using star ground! The key feature of the star ground system is that all voltages are measured with respect to a particular point in the ground network, not just to an undefined "ground" (i.e., wherever one can clip a probe) as shown in image below.  One example for analog and digital where star grounding is most beneficial is in audio circuits where there’s an analog to digital converter and vice-versa. We want to make sure there is a common ground for all analog and digital components.


When the power supplies are added to the circuit diagram, they either add unwanted ground paths, or their supply currents flowing in the existing ground paths are sufficiently so large, or noisy (or both) so as to corrupt the signal transmission. This particular problem can often be avoided by having separate power supplies (and thus separate ground returns) for the various circuit portions. For example, separate analog and digital supplies with separate analog and digital grounds, joined at the star point, are common in mixed signal applications.

## Summary ##
From this blog, I hope you can get some pointers on how to design your grounding for analog and digital circuits. Regardless of whether you are designing analog, digital or mixed signals circuit, good grounding design can help you spend more time on your schematic and other design issues.


Check out my other [works][business] and [other writings][blogs]  to see what I do everyday, or click [here][about] to learn more about me.

[blogs]: http://vincetallica.github.io/blogs
[about]: http://vincetallica.github.io/about
[business]:   https://vpakwong.github.io/
