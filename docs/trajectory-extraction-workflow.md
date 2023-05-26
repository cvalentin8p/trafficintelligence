This page explains the typical workflow if trying different tracking parameters, in relationship to the data storage and the two steps, feature tracking and grouping:

1. The feature grouping step will generate a SQLite database with the positions and velocities table. If running this step another time, you will see in the console repeated "rollback" messages, because the program tries to save the same data, with the same primary key and, rightly, fails. To generate new feature tracking results, one has to rename the SQLite file, change the output `database-filename` parameter or delete the SQLite file. 
    * use the `feature-based-tracking` program with the `--tf` option
2. The feature grouping step adds the tables objects_features and objects to represent the road users as sets of features. Again, if run twice, one will see "rollback" messages. However, since feature tracking is time-consuming while feature grouping runs much faster, if one wants to re-run only the grouping phase, one should not delete/rename the SQLite file or change the output `database-filename` parameter since the features will have to be re-computed. The solution is to delete the tables objects_features and objects either manually (open the database and execute the SQL command `drop table [table_name]`) or through the provided `delete-table.py` script.
    * use the `feature-based-tracking` program with the `--gf` option
    * seeing an error message that the `objects_features` table is missing from your database means you forgot this step
3. **Optional step** if the tracking results are not adequate, you can adjust the tracking parameters in the `tracking.cfg` file, either manually by trial and error or with the `optimize-with-nomad.py` script in the scripts/nomad directory ([details](tracking-optimization.md)).
4. [Classify the road users](road-user-classification.md) into different categories (pedestrian, cyclist, car).

Note that these steps should be done iteratively. You should track and group the features and immediately look at the resulting trajectories. Notably, verify that the projection on the world map is adequate and that the speed distributions are coherent before proceeding with subsequent analyses (prototypes and safety analysis).

Here is a history of commands going through the steps including camera calibration:
```
1008  compute-homography.py -u 0.05208 -i frame.png -w world.png --intrinsic intrinsic-camera-gopro2-uw.txt --distortion-coefficients -0.12 0.0 0.0 0.0 0.0 --undistort -n 6 --undistorted-multiplication 1.3
1010  cat homography.txt
1012  cp ~/Research/Code/traffic-intelligence/tracking.cfg .
1013  cp ~/Research/Code/traffic-intelligence/classifier.cfg .
1015  emacs tracking.cfg&
1020  feature-based-tracking tracking.cfg --tf --display 1
1021  feature-based-tracking tracking.cfg --gf
1022  display-trajectories.py --cfg tracking.cfg
1024  display-trajectories.py --cfg tracking.cfg -t object
1026  delete-tables.py -d G0010128.sqlite -t object
1027  display-trajectories.py --cfg tracking.cfg -t object
1028  feature-based-tracking tracking.cfg --gf
1029  display-trajectories.py --cfg tracking.cfg -t object
1031  display-trajectories.py --cfg tracking.cfg -t object -s 10
1032  classify-objects.py -h
1034  display-trajectories.py --cfg tracking.cfg -t object -s 10
```