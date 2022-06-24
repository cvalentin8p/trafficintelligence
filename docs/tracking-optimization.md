Optimization tool
==============

The tool was developed by Etienne Beauchamp. It will be reworked in the next weeks to streamline it and use Nomad 4. For now, if you want to use the code provided in scripts/nomad, you must use Nomad 3. 

# Usage
1. Make sure your data should be structured something like the following (may be adapted):

```
    Data                        # Folder containing all the data
    └── <Intersection name>     # Intersection (e.g. montcalm-chartwell)
        ├── <tracking configuration file>.cfg
        ├── <Date 1>
        │   ├── <Other subdirectories>    # There can be as many subdirectories as you want
        │       ├── <Video 1>
        │       ├── <Ground truth database 1>_gt.sqlite
        │       ├── homography.txt
        │       ├── image.pg
        │       ├── mask.png
        │       └── point-correspondences.txt
        ├── <Date 2>
        └── <Date 3>
             .
             .
             .
```

**Please note**: You should have at least one ground truth database (with a name ending with `_gt.sqlite`) for each date of the intersection. For now, it is also required to have a tracking configuration file (ending with `.cfg`) for each site to accound for different camera parameters. Future versions will rely on metadata. 

2. Select an intersection or several intersections for which you wish to find optimal tracking parameters, for instance:

```$ python3 optimize-with-nomad.py -t /media/disk2/etienne/Data/montcalm-chartwell/ /media/disk2/etienne/Data/montcalm-victorin/ --optimize-grouping-only```

It may be a good idea to copy the scripts/nomad directory if one wishes to modify the code. 

**Please note**: You need an existing database with good feature trajectories to find the optimal parameters using only the grouping phase of the tracking algorithm. 

3. Once the optimal parameters are found, tracking may be launched with the outputed :

```
$ cd $HOME/Data/montcalm-chartwell
$ feature-based-tracking tracking-visible.cfg --tf --video-filename 2019-11-27/Visible/2019-11-27T12\:20-05\:00.MP4 --database-filename 2019-11-27/Visible/2019-11-27T12\:20-05\:00.sqlite --homography-filename 2019-11-27/Visible/homography.txt --mask-filename 2019-11-27/Visible/mask.png --feature-quality 0.1 --min-feature-distanceklt 3.54964337411 --window-size 6 --min-tracking-error 0.01 --min-feature-time 15
$ feature-based-tracking tracking-visible.cfg --gf --video-filename 2019-11-27/Visible/2019-11-27T12\:20-05\:00.MP4 --database-filename 2019-11-27/Visible/2019-11-27T12\:20-05\:00.sqlite --homography-filename 2019-11-27/Visible/homography.txt --mask-filename 2019-11-27/Visible/mask.png --mm-connection-distance 2 --mm-segmentation-distance 1.9 --min-nfeatures-group 4
```
