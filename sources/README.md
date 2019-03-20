## Running tests

### Training models

Models are trained by running the following command from the R command line:

```r
source('train_all_datasets.R')
```

The datasets, the number and types of models to train are set directly in the script:

Example (training 256 models of 3 different types - CF, xgb and GAM - on 5 different datasets, i.e. a total of 3*256*5 models):
```r
model.types <- c('CF', 'xgb', 'GAM')
dataset.names <- c('bikeShare', 'CO2', 'Irradiance', 'Electricity', 'Traffic')
nb.models <- 256 # number of models to train per type of model and per dataset
```

Three types of models are implemented: Siamese-network based Collaborative Filtering (CF), XGBoost regression trees (xgb) and Generalized additive models (GAMs).
CF models are pretty long to train since it is a custom-based implementation we did in R. A more competitive package concerning these models will be released later.

Trained models are stored on the disk in a local folder of the type: "./predModels_#DATASET_#MODELTYPE/".

### Predicting models

Each trained model is used to predict the test set of each dataset by running the command:

```r
source('test_all_datasets.R')
```

Prediction are stored on the disk in a folder: "./allpreds/".

### Running model selection

Model selection is performed on each dataset by running the command:

```r
source('run_tests.R')
```

The datasets, the number and types of models to select from, as well as the number of run to perform and the baselines to compare to are set directly in the script:

Example (Performing model selection among 3 pools of models of respective sizes 8, 16 and 32 containing models of 2 different types - xgb and GAM - trained on the 'CO2' dataset, and comparing each time with the baselines FS, MLpol, MLewa and EWA):
```r
model.types <- c('xgb', 'GAM')
dataset.run <- 'CO2'
nb.models <- c(8, 16, 32) # number of models to aggregate / select from
baselines.op <- c('FS', 'MLpol', 'MLewa', 'EWA')
N.run <- 1
```

### Performing and end-to-end example run:
A example script can be run that summarizes all the above tests and showcases ther performance of our model selection algorithm:

```r
source('example_use.R')
```

The script takes less than 1 minute to run on an intel core I7, with linux distribution.