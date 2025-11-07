## Parameters
MDE parameters are defined in the MDE constructor. 

| Parameter | Default | Description |
|---|---|---|
| dataFrame | None | Pandas DataFrame : column observation vectors, row observations |
| dataFile | None | Data file name to load |
| dataName | None | Data name in .npz archive |
| removeTime | False | Remove first column from dataFrame |
| noTime | False | First column of dataFrame is not time vector |
| columnNames | [] | dataFrame columns to process |
| initDataColumns | [] | If reading .npz omit these leading columns |
| removeColumns | [] | Columns to ignore |
| D | 3 | Maximum number of MDE dimensions |
| target | None | Target variable |
| lib | [] | EDM library indices. Default to all rows |
| pred | [] | EDM prediction indices. Default to all rows  |
| Tp | 1 | Prediction time interval |
| tau | -1 | CCM embedding time delay |
| exclusionRadius | 0 | CCM library temporal exlcusion radius |
| sample | 20 | CCM random library samples to average |
| pLibSizes | [10, 15, 85, 90] | Percentiles of CCM library sizes |
| noCCM | False | Disable CCM |
| ccmSlope | 0.01 | Slope of CCM(LibSizes) convergence |
| ccmSeed | None | CCM random seed |
| E | 0 | CCM embedding dimension. If 0 compute automatically |
| crossMapRhoMin | 0.5 | Minimum rho for cross map acceptance |
| embedDimRhoMin | 0.5 | Minimum rho for CCM embedding dimension |
| maxE | 15 | Maximum embedding dimension for CCM |
| firstEMax | False | CCM embedding dimension is first local peak in rho(E) |
| timeDelay | 0 | Add N=timeDelay time delays |
| cores | 5 | number of multiprocessing CPU in CrossMapColumns() |
| mpMethod | None | multiprocessing context method in CrossMapColumns() |
| chunksize | 1 | multiprocessing chunksize in CrossMapColumns() |
| outDir | None | Output file directory |
| outFile | None | MDE object pickle file |
| outCSV | None | CSV of MDE output |
| logFile | None | Log file |
| consoleOut | True | Echo output to console |
| verbose | False | Verbose mode |
| debug | False | Debug mode |
| plot | False | Plot MDE result |
| title | None | Plot title |
| args | None | ArgumentParser object from CLI_Parser |
