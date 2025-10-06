---
title: Creative Robot Tool Use by Counterfactual Reasoning
layout: default
---

Consider a TV remote that falls under the sofa where you cannot reach directly. You might look for an object to help retrieve it. Intuitively, you can rule out a book for being too short, a crowbar for being too heavy, or a chair for being too large to fit under the gap. Instead, you might try a rolling pin or a selfie stick. But how do you know which object is suitable for the task? This judgment relies on understanding which physical properties, such as length, weight, or shape, are relevant for the task at hand, and whether a candidate object satisfies those properties. Humans can reason about this effortlessly using prior experience, commonsense knowledge, and an internal model of how physical interactions work.

<figure>
    <div class="figure">
        <div class="subfigure">
        <img src="images/IntroPic.png" alt="Method outline" width="100%">
        </div>
    </div>
    <figcaption><b>Figure 1:</b> An overview of the pipeline. For a given source object and the task definition, a VLM proposes a set of object features that might affect the task success. Using the candidate features as axes of variation, a 3D semantic shape editing tool generates counterfactual objects, and by carrying out the task in simulation, the robot discovers the causal features which then can be used to find out substitutes for creative robot tool use.
    </figcaption>
</figure>

In this work, we show that a similar form of reasoning can be enabled in robots by combining commonsense priors from vision language models (VLMs) with counterfactual reasoning through simulation. We propose **ToolAnalogy**, a novel approach that discovers object properties that are causally related to task success by experimenting with counterfactual objects generated with a 3D semantic object editor, and uses these causal features to classify novel objects as substitutes to carry out the task.

Imagine the three scenarios below where the robot completes the task using a *source* tool.
<figure>
    <div class="figure">
        <div class="subfigure">
            <video width="100%" autoplay loop muted>
                <source src="images/hook.mp4" type="video/mp4">
                Your browser does not support the video tag.
            </video>
            <figcaption style="text-align: center">Hooking</figcaption>
        </div>
        <div class="subfigure">
            <video width="100%" autoplay loop muted>
                <source src="images/reach.mp4" type="video/mp4">
                Your browser does not support the video tag.
            </video>
            <figcaption style="text-align: center">Reaching</figcaption>
        </div>
        <div class="subfigure">
            <video width="100%" autoplay loop muted>
                <source src="images/scoop.mp4" type="video/mp4">
                Your browser does not support the video tag.
            </video>
            <figcaption style="text-align: center">Scooping</figcaption>
        </div>
    </div>
    <figcaption><b>Figure 2:</b> In these three examples, the robot completes the task using (1) a hockey stick to hook an object, (2) a platform to step on, (3) and a spoon to scoop candies with previously acquired skills.</figcaption>
</figure>

What happens when you are in a new environment where the exact source tool is missing? What could you possibly use to hook something, or reach an object on high shelf, or scoop candies? The agent would pick objects based on their features if only it knew which of those features are causally relevant. However, the robot *must* conduct *interventional experiments* to figure out such causal features---experiments that answer questions such as "what happens if the hockey stick happened to be shorter?", "could I stepped on the platform if it was lighter?", or "would a spoon with a flat head work?"

We can now answer these questions using recent advances in computer vision and foundational models. Below are example semantic edits using Ganeshan et al. (2024).

<figure>
    <div class="figure">
        <div class="subfigure">
            <video width="100%" autoplay loop muted>
                <source src="images/hockey-edit.mp4" type="video/mp4">
                Your browser does not support the video tag.
            </video>
        </div>
        <div class="subfigure">
            <video width="100%" autoplay loop muted>
                <source src="images/box-edit.mp4" type="video/mp4">
                Your browser does not support the video tag.
            </video>
        </div>
        <div class="subfigure">
            <video width="100%" autoplay loop muted>
                <source src="images/spoon-edit.mp4" type="video/mp4">
                Your browser does not support the video tag.
            </video>
        </div>
    </div>
    <figcaption><b>Figure 3:</b> Using a semantic object editor, we generate a dataset of <emph>counterfactual</emph> objects by changing the properties of their parts.</figcaption>
</figure>

Once we have a dataset of *counterfactual* objects---objects that are the product of imagination---the robot can test in simulation which of those objects work to figure out the causal features and their boundaries.

<figure>
    <div class="figure">
        <div class="subfigure">
            <video width="100%" autoplay loop muted>
                <source src="images/hook-sim.mp4" type="video/mp4">
                Your browser does not support the video tag.
            </video>
        </div>
        <div class="subfigure">
            <video width="100%" autoplay loop muted>
                <source src="images/spot-sim.mp4" type="video/mp4">
                Your browser does not support the video tag.
            </video>
        </div>
        <div class="subfigure">
            <video width="100%" autoplay loop muted>
                <source src="images/scoop-sim.mp4" type="video/mp4">
                Your browser does not support the video tag.
            </video>
        </div>
    </div>
    <figcaption><b>Figure 4:</b> Test which one of those counterfactual objects work in simulation to find out features that are causally relevant to the task.</figcaption>
</figure>

And after that, having a classifier that is grounded to causal features, the robot can recognize *novel* substitutes to complete the task.
<figure>
    <div class="figure">
        <div class="subfigure">
            <video width="100%" autoplay loop muted>
                <source src="images/hook-novel.mp4" type="video/mp4">
                Your browser does not support the video tag.
            </video>
        </div>
        <div class="subfigure">
            <video width="100%" autoplay loop muted>
                <source src="images/spot-novel.mp4" type="video/mp4">
                Your browser does not support the video tag.
            </video>
        </div>
        <div class="subfigure">
            <video width="100%" autoplay loop muted>
                <source src="images/scoop-novel.mp4" type="video/mp4">
                Your browser does not support the video tag.
            </video>
        </div>
    </div>
    <figcaption><b>Figure 5:</b> Left&mdash;the robot uses a selfie stick (instead of a hockey stick) to pull the object while it correctly classifies that a crowbar would not work as it exceeds the payload threshold. Middle&mdash;Spot uses a box that is hollow inside with different dimensions than the original platform. Right&mdash;after learning the causal features for scooping, the robot can recognize that it can use a paper food tray, an item that is in a completely different category than spoon-like utensils, to scoop something since it is both graspable and have enough head area to contain items.</figcaption>
</figure>

See the [the full video](images/video.mp4).