---
title: About scikit-multiflow
sidebar: false
---

`scikit-multiflow` is an open-source machine learning package for streaming data. It extends the scientific tools available in the Python ecosystem. `scikit-multiflow` is intended for streaming data applications where data is continuously generated and must be processed and analyzed on the go. Data samples are not stored, so learning methods are exposed to new data only once.

The (theoretical) infinite nature of data stream poses additional challenges to learning. Resources such as memory and time are limited, and stream learning methods must efficiently handle resources. Dynamic environment imply that data can change over time, a change in data distribution is known as concept drift. Concept drift results in model degradation if not handled properly. Drift-aware methods are designed to be robust against concept drift. 

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

## Logo

The `scikit-multiflow` logo is based on the design by Vectortwins / Freepik. The font used is Flux Regular.
