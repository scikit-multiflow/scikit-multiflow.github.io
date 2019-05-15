---
layout: single
title: Updated base class to be introduced in release `0.3.0`
toc: False
author_profile: False
category: ['announcement']
tags: ['architecture change', 'upcoming release']
---

## What is happening?
The upcoming release `0.3.0` will introduce an improved base object class `BaseSMKObject` which is consistent with `sklearn.BaseEstimator`.

This is a low-level change with direct impact on most components within `scikit-multiflow`. We have tried to minimize the impact on the end users and this post aims to reduce the uncertainty from this change.

## How does this affects me?
Here are the considerations to have in mind to ensure a smooth transition, depending on your usage of `scikit-multiflow`.

### I am a practitioner
If you are using `scikit-multiflow` methods without modifying them then the change should have minimum impact on your workflow. However some methods' signatures were updated:

`DataStream`
* `cat_features_idx` -> `cat_features`
* `name`: new attribute to define a name for your data

`FileStream`
* `cat_features_idx` -> `cat_features`

`PageHinkley`
* `min_num_instances` -> `min_instances`

`KNN`
* `categorical_list` -> `nominal_attributes`

Similarly, `partial_fit` and `fit` methods where updated for consistency with `scikit-learn` methods:

`weight` -> `sample_weight`

*Note:* "->" means "renamed to"


### I am a developer/researcher
In case that you are modifying the `scikit-multiflow` methods or extending them to create your own methods then there are some considerations to take into account additional to the ones mentioned above.

The `skmultiflow.core.BaseSKMObject` class is the new base class in `scikit-multiflow`. It is based on `sklearn.BaseEstimator` in order to support inter-framework compatibility and adds extra functionality relevant in the context of `scikit-multiflow`.

Stream models (estimators) in `scikit-multiflow` are now created by extending the `BaseSKMObject` class and the corresponding task-specific mixin(s): `ClassifierMixin`, `RegressorMixin`, `MetaEstimatorMixin`, `MultiOutputMixin`

The `ClassifierMixin` defines the following methods:

* `fit` -- Trains a model in a batch fashion. Works as a an interface to batch methods that implement a ``fit()`` functions such as ``scikit-learn`` methods.
* `partial_fit` -- Incrementally trains a stream model.
* `predict` -- Predicts the target's value in supervised learning methods.
* `predict_proba` -- Calculates the probability of a sample pertaining to a given class in classification problems.

The `RegressorMixin` defines the same methods for the regression setting with minor differences in the methods' signatures.


## Further information
If you are interested in finding more about this change you can check the corresponding [issue](https://github.com/scikit-multiflow/scikit-multiflow/issues/45) and [PR](https://github.com/scikit-multiflow/scikit-multiflow/pull/110) in GitHub. Or you can contact us through the [user's group](https://groups.google.com/forum/#!forum/scikit-multiflow-users) or [gitter channel](https://gitter.im/scikit-multiflow/community).