---
layout: single
title: "Installation"
permalink: /installation/
excerpt: "Guide to install scikit-multiflow."
toc: false
author_profile: false
---

**Notice:** `scikit-multiflow` works with Python 3 **only**.

`scikit-multiflow` requires `numpy` to be already installed in your system.
There are multiple ways to install `numpy`, the easiest is using
[`pip`](https://pip.pypa.io/en/stable/#):

``` bash
  $ pip install -U numpy
```

Once `numpy` is installed, we can proceed with the installation of
`skmulti-flow` and its other dependencies. Run the following command in the
 local path where you placed `scikit-multiflow`:

``` bash
  $ pip install -U .
```

After the installation is completed, we can start using `scikit-multiflow`.

### matplotlib backend considerations
* You may need to change your matplotlib backend, because not all backends work
in all machines.
* If this is the case you need to check
[matplotlib's configuration](https://matplotlib.org/users/customizing.html).
In the matplotlibrc file you will need to change the line:  
    ```
    backend     : Qt5Agg  
    ```
    to:  
    ```
    backend     : another backend that works on your machine
    ```  
* The Qt5Agg backend should work with most machines, but a change may be needed.
