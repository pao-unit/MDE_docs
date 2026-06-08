## MDE Class
MDE is an object-oriented class implementation. MDE class arguments can be specified through the MDE class constructor. A command line interface (CLI) is also supported for the MDE and Evaluate classes with CLI parameters configured through command line arguments.

The MDE class can be imported as a module and executed with `dimx.Run()` or from the command line with the`ManifoldDimExpand.py` wrapper as shown in the examples. 

Class and application parameters are detailed in the [parameters](parameters.md) table.

### MDE Class Constructor
MDE class constructor 
```python
MDE( dataFrame       = None,  # pandas DataFrame
     dataFile        = None,  # file name for DataFrame
     dataName        = None,  # dataName in npz archive
     removeTime      = False, # remove dataFrame first column
     noTime          = False, # first dataFrame column is data
     columnNames     = [],    # partial match columnNames
     initDataColumns = [],    # .npy .npz : see ReadData()
     removeColumns   = [],    # columns to remove from dataFrame
     D               = 3,     # MDE max dimension
     target          = None,  # target variable to predict
     lib             = [],    # EDM library start,stop 1-offset
     pred            = [],    # EDM prediction start,stop 1-offset
     Tp              = 1,     # prediction interval
     tau             = -1,    # CCM embedding delay
     exclusionRadius = 0,     # exclusion radius: CCM, CrossMap
     sample          = 20,    # CCM random sample
     pLibSizes       = [10, 15, 85, 90], # CCM libSizes percentiles
     noCCM           = False, # Do not validate with CCM
     ccmSlope        = 0.01,  # CCM convergence criteria
     ccmSeed         = None,  # CCM random seed
     E               = 0,     # Static E for all CCM
     crossMapRhoMin  = 0.5,   # threshold for L_rhoD in Run()
     embedDimRhoMin  = 0.5,   # maxRhoEDim threshold in Run()
     maxE            = 15,    # maximum embedding dim for CCM
     firstEMax       = False, # use first local peak for E-dim
     timeDelay       = 0,     # Number of time delays to add
     crossMapCores   = None,  # cross-map core cap; None=all cores
     mpMethod        = None,  # multiprocessing start context
     chunksize       = 1,     # multiprocessing chunksize
     sharedMem       = 0.1,   # shared-mem threshold (decimal MB)
     logPct          = 0,     # cross-map progress band
     kdWorkers       = 1,     # KDTree.query workers in Simplex
     outDir          = './',  # use pathlib for windog
     outFile         = None,
     outCSV          = None,
     logFile         = None,
     consoleOut      = True,  # LogMsg() print() to console
     verbose         = False,
     debug           = False,
     plot            = False,
     title           = None,
     args            = None )
```

**Required Arguments**

```target``` : target variable

```dataFrame``` or ```dataFile``` : Multivariate observations

**Notes**

MDE includes all columns in the `dataFrame` when scanning observables. To avoid including the `target` or other columns list them in `removeColumns`, for example: `removeColumns=[index, FWD, Left_Right]`. To explicitly list columns to scan `columnNames` can be used.

If the EDM/CCM library (`lib`) and prediction (`pred`) row indices are not specified they default to all observation rows in the dataFrame. This is not suitable for MDE which should use out-of-sample prediction: `pred`∉`lib`.

`ccmSlope` determines the criteria for CCM convergence. It is the slope of a linear regression of CCM predictive correlation onto [0,1] normalized CCM library sizes specified as percentiles in `pLibSizes`.

`crossMapRhoMin` and `embedDimRhoMin` are minimum thresholds of predictive correlation to accept a candidate observation vector as valid (`crossMapRhoMin`) and qualify the embedding dimension for CCM (`embedDimRhoMin`). Higher values make MDE more selective. Default values of 0.5 may be too high for specific data/systems.

The embedding dimension needed for CCM is automatically determined if parameter `E=0`, the default. Otherwise the specified value of `E` is used. 

To account for unobserved variables N = `timeDelay` vectors of the top observables can be added to the manifold. 

---

### MDE Class Methods

```python
Run()
```
Run a configured MDE class instance.

---

## MDE Applications

### Evaluate
Evaluate MDE discovered observables predicting the target. Compare to PCA and 
diffusion map decompositions. 
```python
Evaluate( dataFrame       = None,
          dataFile        = None,
          outFile         = None,
          mde_columns     = [],    # MDE columns
          columns_range   = [],    # (start,stop) indices for data columns
          i_columns       = [],    # list of dataFile column indices for data
          columnMatch     = [],    # list of columns (partial matching) for data
          removeColumns   = [],    # list of columns to ignore in MDE
          removeTime      = False,
          initDataColumns = [],    # insert initial column names
          predictVar      = None,  # target variable
          library         = [],    # EDM lib
          prediction      = [],    # EDM pred
          E               = 0,     # MDE E if adding time delays
          tau             = -1,    # MDE tau if adding time delays
          Tp              = 0,     # EDM prediction horizon
          components      = 3,     # number of PCA, Diffusion Map components
          dmap_k          = 5,     # diffusion map 
          dmap_epsilon    = 'bgh', # diffusion map 
          dmap_alpha      = 0.5,   # diffusion map 
          plot            = False,
          plotRho         = False,
          minMax          = False, # apply min/max scaler to data and pred plot
          maxN            = 7,
          figsize         = (8, 8),
          xlim            = None,
          verbose         = False,
          args            = None )
```

### MDE CLI ManifoldDimExpand.py:
```ManifoldDimExpand.py``` is an executable program that instantiates and 
runs an ```MDE``` class instance. Parameters are detailed in the [parameters](parameters.md) table and can be listed with the ```-h``` command line option.

```
./ManifoldDimExpand.py -d ../data/Fly80XY_norm_1061.csv 
-rc index FWD Left_Right -D 10 -t FWD -l 1 300 -p 301 600
-C 10 -ccs 0.01 -emin 0.5 -P -title "MDE FWD" -v
```
