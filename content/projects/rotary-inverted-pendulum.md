+++
date = '2025-02-24T13:15:05+13:00'
draft = false
title = 'Rotary Inverted Pendulum'
description = 'A simple prototype using a stepper motor, an Arduino Uno and a rotary encoder'
tags = ["Control Systems", "Arduino", "Embedded Systems", "Linear Quadtratic Regulator"]
layout = 'portfolio'
+++

## Introduction
During my last semester as an undergraduate, we were given an group assignment to find suitable gains that would stabilise a linear inverted pendulum for any given position. In our case, the system was a cart on linear rails with a pendulum attached, similar to the image showed below:
[![cart on rails with a pendulum](/rotary-inverted-pendulum/cart-pendulum-wiki.png)](https://en.wikipedia.org/wiki/File:Cart-pendulum.svg)

We were given a state-space model of the system and used the linear quadratic regulator (LQR) method to find suitable gains through MATLAB simulations. Once we believed we found our gains, we could try them out on a real cart-pendulum system that was set up at the university.

However, despite eventually finding suitable gains as a group, I felt I didn't understand the theory enough to be able to apply it to a real-world system by myself. So, I decided to create a prototype that would allow me to do just that. I felt a rotary (rather than linear) inverted pendulum would be mechanically simpler and take up less space. However, the mathematics is more complicated due to a greater number of non-linear terms. But that's what the summer is for and I'm here to learn!


You can find the full documentation, hardware details and software details at **[Github](https://github.com/jensen-benard/rotary-inverted-pendulum.git)**.

## Demonstration

## System Overview