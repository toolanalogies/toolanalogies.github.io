---
title: Creative Robot Tool Use by Counterfactual Reasoning
layout: default
---

Consider a TV remote that falls under the sofa where you cannot reach directly. You might look for an object to help retrieve it. Intuitively, you can rule out a book for being too short, a crowbar for being too heavy, or a chair for being too large to fit under the gap. Instead, you might try a rolling pin or a selfie stick. But how do you know which object is suitable for the task? This judgment relies on understanding which physical properties, such as length, weight, or shape, are relevant for the task at hand, and whether a candidate object satisfies those properties. Humans can reason about this effortlessly using prior experience, commonsense knowledge, and an internal model of how physical interactions work.

<figure style="width: 100%; margin: auto; padding: 0">
    <img src="images/IntroPic.png" alt="Method outline" width="100%">
</figure>

In this work, we show that a similar form of reasoning can be enabled in robots by combining commonsense priors from vision language models (VLMs) with counterfactual reasoning through simulation. We propose **ToolAnalogy**, a novel approach that discovers object properties that are causally related to task success by experimenting with counterfactual objects generated with a 3D semantic object editor, and uses these causal features to classify novel objects as substitutes to carry out the task.


<figure style="display: flex; gap: 10px; flex-wrap: wrap; width: 100%; margin: auto; padding: 0">
    <div style="flex: 1">
        <video width="100%" autoplay loop muted style="flex: 1">
            <source src="images/hook.mp4" type="video/mp4">
            Your browser does not support the video tag.
        </video>
        <figcaption style="text-align: center">Hooking</figcaption>
    </div>
    <div style="flex: 1">
        <video width="100%" autoplay loop muted style="flex: 1">
            <source src="images/reach.mp4" type="video/mp4">
            Your browser does not support the video tag.
        </video>
        <figcaption style="text-align: center">Reaching</figcaption>
    </div>
    <div style="flex: 1">
        <video width="100%" autoplay loop muted style="flex: 1">
            <source src="images/scoop.mp4" type="video/mp4">
            Your browser does not support the video tag.
        </video>
        <figcaption style="text-align: center">Scooping</figcaption>
    </div>
</figure>

