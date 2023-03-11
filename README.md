# About
#### This repo is designed to show how to synthesize data using gaussian, continuous, and log normal distributions.  I was inspired to make this to show how I would approach solving the cheater problem in the popular FPS PC game, "Escape from Tarkov".  Assuming BSG has a labeled dataset of player names that have cheated versus normal non-cheating players, this approach is feasible.  I would reccomend BSG run a batch daily inference job on player statistics to flag potential cheaters for further investigation.  Since we don't have the data, most of this code is synthesizing reasonable data and labeling it as a cheater or non-cheater accordingly.

## Technical high-level

#### I create two datasets, one for cheaters, one for honest players.  I then join them and randomly shuffle the data.  The cheater dataframe and honest player dataframe both have the same columns.  With the current version of the code, there's 100k honest players and 5k cheaters.

#### Almost all of the stats are normally distributed.  Some have a 50/50 chance (like for account type).  The notebook prints out histograms of the distributions of the each columns.

#### The model used is a Random Forest Classifier from SKLearn.  Since the data distributions are so obviously different, the model performs very well.  Real player data is likely much more ambigious and would take a professional modeler a lot of time to produce something with good model metrics for this problem.

#### The most important metric is arguably precision, which is the ability of the model to not miss positive samples (cheaters).  Second to that would be recall, which is the ability of the model to label a positive sample as negative (reducing the likelihood of a false positive).  Too many false positives would create an unecessary burden on BSG.

## Run the code
* Create a virtual env
```
python -m venv env
```

* activate a venv
```
source env/bin/activate
```

* install dependencies
```
pip install -r requirements.txt
```

* Run the code in the notebook after pointing the kernel to the newly created virtual env