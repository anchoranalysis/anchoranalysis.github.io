---
title: "Download"
keywords: download anchor image analysis microscopy
tags: [getting_started]
sidebar:
permalink: download.html
hide_sidebar: true
toc: false
disable_editme: true
---

Anchor can be downloaded as a distribution (*zip* or *tar.gz*). This must be unpacked into a directory, followed by setting some environment variables.

Please download the latest version (`anchor-1.2.0`) from GitHub, as matches your operating system:

- [Windows EXE installer](https://github.com/anchoranalysis/anchor-assembly/releases/download/1.2.0/Anchor-1.2.0.exe)
- [Linux DEB package](https://github.com/anchoranalysis/anchor-assembly/releases/download/1.2.0/anchor_1.2.0_amd64.deb) - type `sudo dpkg -i anchor_1.2.0_amd64.deb` and then `sudo apt-get --fix-broken install`
- [MacOS](https://github.com/anchoranalysis/anchor-assembly/releases/download/1.2.0/anchor-1.2.0.pkg)
- [OS Neutral](https://github.com/anchoranalysis/anchor-assembly/releases/download/1.2.0/anchor-1.2.0.zip) - requires installation of a system [JRE](https://www.java.com/en/download/) (>= v21).

{% include tip.html content="After downloading, please follow the [Installation Guide](installation.html)." %}

## Licensing {#licensing}

Most components of Anchor are licensed under the permissive open-source MIT License. A small number are licensed under the less-permissive GPLv3. As a hybrid of both, the Anchor distribution is GPLv3 licensed. Please see the `LICENSE.txt` in each repository and distribution.

## Acknowledgements

Anchor's author is [Owen Feehan](http://www.owenfeehan.com/). Particular additional thanks to:

* [ETH Zurich](https://ethz.ch/en.html), the late [Prof. Wilhelm Krek](https://mhs.biol.ethz.ch/research/krek/biography-krek.html) in whose lab the software originated for analyzing microscopy images.
* Many members of the [Institute of Molecular Health Sciences](https://mhs.biol.ethz.ch/) who kindly helped in associated research and became the first users, and similarly Dr. Naemi Luithle.
* The [University of Zurich](https://www.uzh.ch/en.html) where further development occurred with particular thanks to [Dr. Lars Malmstrom](http://2ddb.org/).
* [Hoffmann-La Roche](https://www.roche.com/) with usage and advancement across several imaging projects.

Many additional [acknowledgements](acknowledgements.html) are owed to the many libraries it publicly depends on.