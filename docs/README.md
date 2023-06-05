Traffic Intelligence Project
==============

# News
* July 1st 2021: the Linux repository version of the OpenCV library (tested on Ubuntu) is sufficient to compile the tracker. 
* After Bitbucket shut down mercurial repositories in the Summer of 2020, here are the solutions I found. I strongly prefer Mercurial to Git, so will keep the code in this version control system, self-hosted for now at [http://132.207.98.161:3000](http://132.207.98.161:3000). I will keep this repository to link things and put the documentation back up in the main repository in the docs sub-directory.
    * Main self-hosted [Traffic Intelligence Mercurial repository](http://132.207.98.161:3000/)
    * The Trajectory management and analysis tool project used to be separately hosted and is now integrated in the main Traffic Intelligence repository after Btibucket gave up on Mercurial.
* February 2nd 2019: The C++ code has been updated to OpenCV4 (you also need to update the [trajectory management and analysis library](https://bitbucket.org/trajectories/trajectorymanagementandanalysis)). Python code seem to need no update as tests are passed. 
* [Past News](past-news.md)

To receive automatically updates and announcements, please register on the [Yahoo Group](https://groups.yahoo.com/neo/groups/traffic-intelligence): it is lightly used, but I have not decided whether to keep it or not.

# Introduction

Welcome the homepage of the Traffic Intelligence project. This software project provides a set of tools developed by [Nicolas Saunier](https://nicolas.saunier.confins.net) and his collaborators for transportation data processing, in particular road traffic, motorized and non-motorized. The project consists in particular in tools for the most typical transportation data type, trajectories, i.e. temporal series of positions. The original work targeted automated road safety analysis using video sensors. 

This software is being developed for many projects and purposes. This project contains:

* C++ code under the c and include directories: a feature-based moving object tracking tool (and very old examples of the use of the [OpenCV](https://opencv.org) and [KLT libraries](https://www.ces.clemson.edu/~stb/klt))
* Python modules for several applications
    * classes for trajectories and moving objects (objects with some characteristics and a series of time-stamped positions): this growing body of code allows the interpretation of trajectory data produced by the C++ video analysis code
        * scripts for specific tasks, e.g. tools to visualize data or examples of data processing ([[Description of Scripts|list of scripts with short description]]) 
    * some basic code for simple traffic engineering problems (fundamental diagram and traffic signal timing)

# Guides

* **[Frequently Asked Questions](faq.md)**
* Compilation and programming environment
    * [Programming style guide](http://wiki.polymtl.ca/transport/index.php/ProgrammingStyle)
    * [Compilation instructions](cpp-compilation.md) for the C++ code, in particular feature-based tracking
	* It is highly recommended to clone the repository to get the latest version of the Python library `trafficintelligence` (but a less frequently updated version is available through pip: `pip install trafficintelligence`) 
    * [[Install and Use the Python Modules and Scripts|How to use the provided Python modules and scripts]]: how to install a Python scientific distribution with the right modules, get and install the Python modules and scripts of Traffic Intelligence.
    * [[How to update configuration file|How to update configuration files]] (when a new program version requires to change the configuration file)
* Data formats
    * [[Data Formats|Data formats]], especially the tables and fields in SQLite
* Step-by-step examples:
    * [Tutorial and information](camera-calibration.md) on camera calibration, homographies (how to use the provided script to create a homography) and distortion
    * [Tutorial](video-tracking-tutorial.md) to extract road user trajectories from video data
    * [Typical workflow](trajectory-extraction-workflow.md) to extract road user trajectories
    * [Steps](tracking-optimization.md) to optimize tracking after cleaning the tracker output trajectories, eg using the [trajectory annotation tool](https://bitbucket.org/Wendlasida/trafficintelligenceannotationtool/) by Tertuis Ou�draogo
    * (Python) [[Loading NGSIM Data using Python Libraries|Simple example of loading road user trajectories from the NGSIM dataset]]
    * (Python) [Tutorial to load and visualize some video tracking results](loading-trajectory-data-extracted-from-video-using-trafficintelligence-python-library.ipynb)
    * (Python) [Tutorial to detect a trajectory crossing a line or polygon](detecting-line-polygon-crossing.ipynb)
    * (Python) [Road User Classification](road-user-classification.md) implemented for road user classification
    * (Python) How to measure [Tracking Performance](tracking-performance.md) (CLEAR MOT metrics)

# Compiled Video Analysis Binary for Windows

Linux is the preferred development platform. All Python code should work on all platforms where the required Python libraries are available. 

Old 32 bit Windows binaries for the tracker can still be found on the Bitbucket Mercurial archive provided by the nice people of Octobus (https://bitbucket-archive.softwareheritage.org/new-static/b5/b54b11eb-b7e2-4791-911d-c2aa3ccb07c5/attachments/). Please volunteer to contribute Windows binaries for the tracker.

# Contribution

We are very interested in outside contributions and to start a collective effort to make video analysis more accessible and widespread in transportation applications. Do not hesitate to contact [Nicolas Saunier](https://nicolas.saunier.confins.net) and to give **feedback** on the code, documentation, etc. **When you find an error** and have a workaround, please send a message about the error so that others will not be stuck in the same place. 

# License

The code is licensed under the [MIT open source license](http://www.opensource.org/licenses/mit-license).

# Acknowledgement

Funding for these developments comes partially through the funding of the students listed on the [contributors' page](contributors.md), supported by NSERC Grant No 402320-2011, FRQNT-MTQ-FRQS grant 2012-SO-163493 (road safety research program 2011-2014) and several MTQ research contracts.

If you make use of this piece of software, please cite one of [our papers](https://nicolas.saunier.confins.net/#publications), for example

* for the tracking software, S. Jackson, L. Miranda-Moreno, P. St-Aubin, and N. Saunier. A flexible, mobile video camera system and open source video analysis software for road safety and behavioural analysis. Transportation Research Record: Journal of the Transportation Research Board, 2365:90-98, 2013 https://dx.doi.org/10.3141/2365-12
* for surrogate road safety analysis N. Saunier, T. Sayed and K. Ismail. Large Scale Automated Analysis of Vehicle Interactions and Collisions. Transportation Research Record: Journal of the Transportation Research Board, 2147:42-50, 2010 https://dx.doi.org/10.3141/2147-06

We would be very happy in any case to know about any use of the code, and to discuss any opportunity for collaboration. 

Contact me at nicolas.saunier[at]polymtl.ca and learn more about our work at [https://nicolas.saunier.confins.net](https://nicolas.saunier.confins.net).

Contributors are listed on this [page](contributors.md).
