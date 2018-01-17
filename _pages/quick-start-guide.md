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

## First example.

Inthis example, we will use a data stream to train a `Hoeffding Tree (VFDT)`
classifier and will measure its performance using prequential evaluation:

1. Create a stream

    The `WaveformGenerator` generates by default instances with 21 numeric
    attributes and 3 targets, based on a random differentiation of some base
    waveforms:

    ``` python
    stream = WaveformGenerator()
    ```

    Before using the stream, we need to *prepare it* by calling
    `prepare_for_use()`:

    ``` python
    stream.prepare_for_use()
    ```

2. Instantiate the Hoeffding Tree classifier

    Use default parameters.

    ``` python
    classifier = HoeffdingTree()
    ```

3. Setup the evaluator
    ``` python
    eval = EvaluatePrequential(show_plot=True, pretrain_size=1000, max_instances=100000)
    ```
    * `show_plot=True` to get a dynamic plot that is updated as the classifier is
    trained.
    * `pretrain_size=1000` sets the number of samples passed in the first train
      call.
    * `max_instances=100000` sets the maximum number of samples to use.

4. Run the evaluation

    By calling `eval()`, we pass control to the *evaluator*, which will perform
    the following sub-tasks:
    * Check if there are instances in the stream
    * Pass the next instance to the classifier:
      - test the classifier (using `predict()`)
      - update the classifier (using `partial_fit()`)
    * Update the plot

    ``` python
    eval.eval(stream=stream, classifier=pipe)
    ```

**Putting it all together:**

``` python
from skmultiflow.data.generators.waveform_generator import WaveformGenerator
from skmultiflow.classification.trees.hoeffding_tree import HoeffdingTree
from skmultiflow.evaluation.evaluate_prequential import EvaluatePrequential

# 1. Create a stream
stream = WaveformGenerator()
stream.prepare_for_use()

# 2. Instantiate the HoeffdingTree classifier
ht = HoeffdingTree()

# 3. Setup the evaluator
eval = EvaluatePrequential(show_plot=True, pretrain_size=1000, max_instances=100000)

# 4. Run evaluation
eval.eval(stream=stream, classifier=ht)
```

**Note:** Since we set `show_plot=True`, a new window will be created for the
plot:

![ classifier_plot](../assets/images/example_classifier_plot.gif)


## Load data from a file as a stream and save test results into a file.

There are cases where we want to use data stored in files. In this example we
will train the same classifier from the First Example, but this time we will
read the data from a (csv) file and will write the predictions to a (csv) file.

1. Load the dataset as a stream

    For this purpose we will use the following:

    ``` python
    options = FileOption(option_value="../datasets/covtype.csv", file_extension="CSV")
    stream = FileStream(file_options)
    ```

    The `FileStream` will generate a stream using the data contained in the file
    defined in `FileOptions`:
    * `option_value="../datasets/covtype.csv"` indicates the path to the file.
    * `file_extension="CSV"` indicates the type of file.

    Once again, before using the stream, we need to *prepare it* by calling
    `prepare_for_use()`:

    ``` python
    stream.prepare_for_use()
    ```

2. Instantiate the Hoeffding Tree classifier

    Use default parameters.

    ``` python
    classifier = HoeffdingTree()
    ```

3. Setup the evaluator

    ``` python
    eval = EvaluatePrequential(pretrain_size=1000, max_instances=100000, output_file='results.csv')
    ```

    * `pretrain_size=1000` sets the number of samples passed in the first train
      call.
    * `max_instances=100000` sets the maximum number of samples to use.
    * `output_file='results.csv'` indicates that the results should be stored
     into a file. In this case a file *results.csv* will be created in the
     current path.

4. Run the evaluation

    By calling `eval()`, we pass control to the *evaluator*, which will perform
    the following sub-tasks:
    * Check if there are instances in the stream
    * Pass the next instance to the classifier:
     - test the classifier (using `predict()`)
     - update the classifier (using `partial_fit()`)
    * Write results to `output_file`

When the test finishes, the *results.csv* file will be available in the current
path. The file contains information related to the test that generated the file.
For this example:

> \# SETUP BEGIN \
  \# File Stream: file_name: ../datasets/covtype.csv  -  num_classes: 7  - num_classification_tasks: 1 \
  \# Prequential Evaluator: n_wait: 200 - max_instances: 100000 - max_time: inf - output_file: results.csv - batch_size: 1 - pretrain_size: 1000 - task_type: classification - show_plotFalse - plot_options: ['performance' \
  \# SETUP END

Result data in the file includes:
* `x_count`: the number of the instance that was used for testing
* `global_performance`: overall performance (accuracy)
* `sliding_window_performance`: sliding window performance (accuracy)
* `global_kappa`: overall kappa statistics
* `sliding_window_kappa`: sliding window kappa statistics

**Putting it all together:**

``` python
from skmultiflow.options.file_option import FileOption
from skmultiflow.data.file_stream import FileStream
from skmultiflow.classification.trees.hoeffding_tree import HoeffdingTree
from skmultiflow.evaluation.evaluate_prequential import EvaluatePrequential

# 1. Create a stream
options = FileOption(option_value="../datasets/covtype.csv", file_extension="CSV")
stream = FileStream(file_options)

# 2. Instantiate the HoeffdingTree classifier
ht = HoeffdingTree()

# 3. Setup the evaluator
eval = EvaluatePrequential(pretrain_size=1000, max_instances=100000, output_file='results.csv')

# 4. Run evaluation
eval.eval(stream=stream, classifier=ht)
```
