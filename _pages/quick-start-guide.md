---
layout: single
title: "Quick-Start Guide"
permalink: /quick-start-guide/
excerpt: "A guide to start using scikit-multiflow."
toc: True
toc_label: "On this page"
toc_icon: "gear"
author_profile: false
---

In this tutorial we show how to use *scikit-multiflow*.

## Basic example

In our first example, we use a data stream to train a `Hoeffding Tree
(VFDT)` classifier and measure its performance using prequential evaluation:

1. Create a stream
For this example we will use the `WaveformGenerator` with default options.
It will generate instances with 21 numeric attributes and 3 targets, based
on a random differentiation of some base waveforms.:

    ``` python
    stream = WaveformGenerator()
    ```
Before using the stream, we need call `prepare_for_use()`:

    ``` python
    stream.prepare_for_use()
    ```

2. Instantiate the HoeffdingTree classifier
For this step we will use the default parameters.

    ``` python
    classifier = HoeffdingTree()
    ```

3. Setup the evaluator
    ``` python
    eval = EvaluatePrequential(show_plot=True, pretrain_size=1000, max_instances=100000)
    ```
  * `show_plot=True` to get a live plot as the classifier is trained
  * `pretrain_size=1000` sets the minimum number of samples before the first evaluation
  * `max_instances=100000` to indicate the maximum number of samples to use

4. Run the evaluation
By calling `eval()` the *evaluator* will perform the following tasks:

* Check if there are instances in the stream
* Pass the next instance to the classifier:
  - to test the classifier (using `predict()`)
  - to update the classifier (using `partial_fit()`)

``` python
eval.eval(stream=stream, classifier=pipe)
```

**Putting it all together:**

``` python

  from skmultiflow.data.generators.waveform_generator import WaveformGenerator
  from skmultiflow.classification.trees.hoeffding_tree import HoeffdingTree
  from skmultiflow.evaluation.evaluate_prequential import EvaluatePrequential

  # 1. Create a stream
  WaveformGenerator()
  stream.prepare_for_use()

  # 2. Instantiate the HoeffdingTree classifier
  ht = HoeffdingTree()

  # 3. Setup the evaluator
  eval = EvaluatePrequential(show_plot=True, pretrain_size=1000, max_instances=100000)

  # 4. Run
  eval.eval(stream=stream, classifier=ht)

```

Since we set `show_plot=True`, a dynamic plot will be displayed in a new window:

![ classifier_plot](../assets/images/example_classifier_plot.gif)
