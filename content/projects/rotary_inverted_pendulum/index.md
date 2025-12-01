---
title : A custom rotary inverted pendulum
type : project
date: 2025-11-30
tags: ["control systems", "LQR", "embedded systems", "stability", "Arduino", "stepper motor", "C++", "Python", "mathematical modelling", "practical"]
categories: ["showcase"]
description : Design and assembly of a simple rotary inverted pendulum using cheap off-the-shelf parts.
draft: false
---

## For education
In the last year of my degree, I was introduced to modern control systems. Naturally, courses have to be rushed to get through as much of the content as possible; I wasn't satisfied with my understanding of the material. Over the summer of 2024 to 2025, I decided to work on a project that would improve my understanding of linear control systems, or at least give me a platform that I could experiment with. A balancing apparatus would be perfect as a project. In fact, one of the most common control systems projects is a linear inverted pendulum:

<figure>
    <img style="display: block; margin: auto; width: 30%; background-color: white" src="https://upload.wikimedia.org/wikipedia/commons/thumb/0/00/Cart-pendulum.svg/330px-Cart-pendulum.svg.png"/> 
    <figcaption style="text-align: center">
        Diagram of a linear inverted pendulum. 
        <a href="https://en.wikipedia.org/wiki/Inverted_pendulum" target="_blank">
        {{< icon "external_link" >}}
        </a>
    </figcaption>
</figure>

A cart is moved in one axis to balance a pendulum vertically. This is similar to balancing a pencil vertically on your finger. But given that my workspace is small and the linear inverted pendulum requires many more parts, a rotary inverted pendulum was more appropriate:

<figure>
    <img style="display: block; margin: auto; width: 30%" src="https://upload.wikimedia.org/wikipedia/commons/thumb/f/f0/RotaryInvertedPendulum.JPG/250px-RotaryInvertedPendulum.JPG"/> 
    <figcaption style="text-align: center">
        A rotating inverted pendulum from wikipedia
        <a href="en.wikipedia.org/wiki/Furuta_pendulum" target="_blank">
        {{< icon "external_link" >}}
        </a>
    </figcaption>
</figure>

Unlike the linear variant, a rotary inverted pendulum rotates the base instead of moving it horizontally, making it much more compact. No need for pulleys, chassis or extra space. The base can be simply rotated directly via a motor or through gearing.

## Demonstration
<figure>
    <video style="display: block; margin: auto" width="60%" controls>
        <source src="rotary_inverted_pendulum_demo_lqr.mp4" type="video/mp4">
        Your browser does not support the video tag.
    </video>
    <figcaption style="text-align: center">
        My rotary inverted pendulum project in action.
    </figcaption>
</figure>

{{< alert >}}
Apologies for the bad lighting and quality. I was using a camera from the 2000s and my ring light wasn't bright enough. But it definitely gives it a vibe.
{{< /alert >}}


The mechanical side of the build is simple. A motor drives a vertical shaft connected to a flange, which then links to a horizontal shaft and the pendulum:

<figure>
    <img style="display: block; margin: auto; width: 80%" src="mechanical_diagram_annotated.jpg"/> 
    <figcaption style="text-align: center">
        Simplified diagram of the rotary inverted pendulum.
    </figcaption>
</figure>

The rig needs a rigid 90 degree connection between the horizontal shaft and the pendulum. Since I couldn't find a shaft with a fixed right-angle bend, I used a universal joint coupler instead:

<figure>
    <img style="display: block; margin: auto; width: 80%" src="https://i0.wp.com/www.theengineeringchoice.com/wp-content/uploads/2021/10/universal-joint.jpg?fit=1280%2C720&amp;ssl=1"/> 
    <figcaption style="text-align: center">
        An example of the universal joint coupler I am using.
        <a href="https://www.theengineeringchoice.com/what-is-universal-joint/" target="_blank">
            {{< icon "external_link" >}}
        </a>
    </figcaption>
</figure>

These couplers are free to swivel as they rotate, which would cause the pendulum to bend in this manner:


<figure>
    <img style="display: block; margin: auto; width: 80%" src="mechanical_diagram_bent.jpg"/> 
    <figcaption style="text-align: center">
        Bent pendulum angle.
    </figcaption>
</figure>

This is undesirable, so I ziptied the pendulum and horizontal shaft together.

Regarding the electronics, I used a stepper motor driven by a stepper driver. An Arduino Uno controls the stepper driver and processes the control algorithm.
In addition, the rotary encoder is read directly by the Arduino Uno.

## Bill of Materials
The total cost of the project, including electronics, summed to **142.44 NZD**.

### Mechanical
| Item | Quantity | Cost (NZD) | Source |
| --- | --- | --- | --- |
| Linear Shaft, 150mm length, 5mm diameter | 1 | $4.17 | [Aliexpress](https://www.aliexpress.com/item/1005006293171727.html) |
| Rigid Shaft Coupler, 5mm to 5mm | 1 | $4.79 | [Aliexpress](https://www.aliexpress.com/item/1005001711245599.html) |
| Rigid Shaft Coupler, 4mm to 6mm | 1 | $4.46 | [Aliexpress](https://www.aliexpress.com/item/1005001711245599.html) |
| Universal Shaft Joint Coupler, 4mm to 4mm | 1 | $3.53 | [Aliexpress](https://www.aliexpress.com/item/1005006861800732.html) |
| Rotary Encoder Mounting Bracket | 1 | $27.74 | [Aliexpress](https://www.aliexpress.com/item/32962680053.html) |
| Linear Shaft, 125mm length, 4mm diameter | 2 (from 5pcs set) | $7.36 | [Aliexpress](https://www.aliexpress.com/item/1005005477259278.html) |
| Rigid Flange Coupler, 5mm | 1 (from 3pcs set) | $14.94 | [BigFace](https://www.bigface.co.nz/item/2009130) |

### Electronics
| Item | Quantity | Cost (NZD) | Source |
| --- | --- | --- | --- |
| Incremental Rotary Encoder 38S6G5-B-G24N 1000ppr | 1 | $26.34 | [Aliexpress](https://www.aliexpress.com/item/1005005071771659.html) |
| Stepper Motor Nema 17 17HE19-2004S | 1 | $27.41 | [Aliexpress](https://www.aliexpress.com/item/1005004731197516.html)  |
| Stepper Motor Driver TMC2209 | 1 | $5.87 | [Aliexpress](https://www.aliexpress.com/item/1005004614528741.html) <sup><a href="#note1">1</a></sup> |
| Arduino Uno | 1 | $20 | ? <sup><a href="#note2">2</a></sup> |

### Notes
<div id="notes">
<ol>
<li id="note1">I couldn't get the UART communication working but the STEP/DIR functionality worked just fine, which is all I needed.</li>
<li id="note2">I reused an Arduino Uno I bought a long time ago, so the price is estimated.</li>
</ol>
</div>

<!-- ## Design choices

## Controls -->




