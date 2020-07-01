---
title: About scikit-multiflow
sidebar: false
---

`scikit-multiflow` is an open-source machine learning package for streaming data. It extends the scientific tools available in the Python ecosystem. `scikit-multiflow` is intended for streaming data applications where data is continuously generated and must be processed and analyzed on the go. Data samples are not stored, so learning methods are exposed to new data only once.

The (theoretical) infinite nature of data stream poses additional challenges. While data in unbounded, resources such as memory and time are limited, therefore stream learning methods must be efficient. Additionally, dynamic environments imply that data can change over time. The change in the distribution of data is known as concept drift and can lead to model performance degradation if not handled properly. Drift-aware stream learning methods are especially designed to be robust against this phenomenon.

## Ecosystem

`scikit-multiflow` is part of the stream learning ecosystem. Other tools include [`MOA`](https://moa.cms.waikato.ac.nz/), the most popular open source  machine learning framework for data streams, and [`MEKA`](http://meka.sourceforge.net/), an open source implementation of methods for multi-label learning. Both `MOA` and `MEKA` are written in Java.

In Python, `scikit-multiflow` complements packages such as `scikit-learn`, whose primary focus is batch learning.

## Development team
Development of  `scikit-multiflow` is performed by the development team and the open-source community. Current members of the development team (in alphabetical order):

* Albert Bifet
* Fabrício Ceschin
* Heitor Murilo Gomes
* Saulo Martiello Mastelini (maintainer)
* Jacob Montiel (maintainer)
* Jesse Read

A list including past members and major contributors is available [here](https://github.com/scikit-multiflow/scikit-multiflow/blob/master/AUTHORS.md). We also acknowledge the [individual members](https://github.com/scikit-multiflow/scikit-multiflow/graphs/contributors) of the open-source community who have contributed to this project.

## Citing

If `scikit-multiflow` has been useful for your research and you would like to cite it in an academic publication, please use the following [paper](http://jmlr.org/papers/v19/18-251.html) ([bibtex](misc/skmultiflow.bib)):

> Montiel, J., Read, J., Bifet, A., & Abdessalem, T. (2018). Scikit-multiflow: A multi-output streaming framework. The Journal of Machine Learning Research, 19(72):1−5.

## Logo

The `scikit-multiflow` logo is based on the design by Vectortwins / Freepik. The font used is Flux Regular.