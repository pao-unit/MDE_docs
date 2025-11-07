## MDE Class
MDE is an object-oriented class implementation. MDE class arguments can be specified through the MDE class constructor. A command line interface (CLI) is also supported for the MDE and Evaluate classes with CLI parameters configured through command line arguments.

The MDE class can be imported as a module and executed with `dimx.Run()` or from the command line with the`ManifoldDimExpand.py` wrapper as shown in the examples. 

Class and application parameters are detailed in the [parameters](parameters.md) table.

### MDE Class Constructor
MDE class constructor 
```python
MDE( dataFrame=None, dataFile=None, dataName=None, removeTime=False,
     noTime=False, columnNames=[], initDataColumns=[], removeColumns=[],
     D=3, target=None, lib=[], pred=[], Tp=1, tau=-1, exclusionRadius=0,
     sample=20, pLibSizes=[10, 15, 85, 90], noCCM=False, ccmSlope=0.01,
     ccmSeed=None, E=0, crossMapRhoMin=0.5, embedDimRhoMin=0.5, maxE=15,
     firstEMax=False, timeDelay=0, cores=5, mpMethod=None, chunksize=1,
     outDir='./', outFile=None, outCSV=None, logFile=None, consoleOut=True,
     verbose=False, debug=False, plot=False, title=None, args=None )
```

**Required Arguments**

```target``` : target variable

```dataFrame``` or ```dataFile``` : Multivariate observations

**Notes**

MDE includes all columns in the `dataFrame` when scanning observables. To avoid including the `target` or other columns list them in `removeColumns`, for example: `removeColumns=[index, FWD, Left_Right]`. To explicitly list columns to scan `columnNames` can be used.

If the EDM/CCM library (`lib`) and prediction (`pred`) row indices are not specified they default to all observation rows in the dataFrame.

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
Evaluate( dataFrame=None, dataFile=None, outFile=None, mde_columns=[], 
          columns_range=[], i_columns=[], columnMatch=[], removeColumns=[],
          removeTime=False, initDataColumns=[], predictVar=None, library=[],
          prediction=[], E=0, tau=-1, Tp=0, components=3, dmap_k=5,
          dmap_epsilon='bgh', dmap_alpha=0.5, plot=False, plotRho=False,
          minMax=False, maxN=7, figsize=(8, 8), xlim=None, verbose=False,
          args=None )
```

### MDE CLI ManifoldDimExpand.py:
```ManifoldDimExpand.py``` is an executable program that instantiates and 
runs an ```MDE``` class instance. Parameters are detailed in the [parameters](parameters.md) table and can be listed with the ```-h``` command line option.

```
./ManifoldDimExpand.py -d ../data/Fly80XY_norm_1061.csv 
-rc index FWD Left_Right -D 10 -t FWD -l 1 300 -p 301 600
-C 10 -ccs 0.01 -emin 0.5 -P -title "MDE FWD" -v
```
