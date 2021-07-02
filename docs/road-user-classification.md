Various methods are available to classify tracked road users. 

* Speed-based classification: use the `classifyUserTypeSpeed` method in the `MovingObject` Python class
* Classification based on frequency analysis of speed profiles (see Saunier, N.; El Husseini, A.; Ismail, K.; Morency, C.; Auberlet, J.-M. & Sayed, T. Pedestrian Stride Frequency and Length Estimation in Outdoor Urban Environments using Video Sensors. Transportation Research Record: Journal of the Transportation Research Board, 2011, 2264, 138-147, [preprint](http://n.saunier.free.fr/saunier/stock/saunier11pedestrian-stride.pdf)
* Classification based on appearance (being implemented from Zangenehpour, S.; Miranda-Moreno, L. F. & Saunier, N. Automated Classification in Traffic Video at Intersections with Heavy Pedestrian and Bicycle Traffic. Transportation Research Board Annual Meeting Compendium of Papers, 2014): see methods `classifyUserTypeSpeed` and `classifyUserTypeHoGSVM`, as well as the `classify-objects.py` scripts (and another to train the classifiers). 
    * SVM classifiers trained on [examples](../data/training.tar.bz2) of the three classes (pedestrians, vehicles, cyclists) are available in the [data](../data/svm-ped-cyc-car.tar.bz2)
	* one needs the `classifier.cfg` configuration file from the Traffic Intelligence repository properly configured. 

