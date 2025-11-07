## MDE Class
MDE is an object-oriented class implementation. MDE class arguments can be specified through the MDE class constuctor. A command line interface (CLI) is also supported for the MDE and Evaluate classes. CLI parameters are configured through command line arguments.

MDE can be imported as a module and executed with `dimx.Run()` or from the command line with the`ManifoldDimExpand.py` as shown in the examples. 

Class and application parameters are detailed in the [parameters](parameters.md) table.

### MDE Class Constructor
MDE class constuctor 
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


### MDE Class Methods

```python
Run()
```
Run a configured MDE class instance.

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
