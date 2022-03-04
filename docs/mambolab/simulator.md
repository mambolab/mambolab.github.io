---
layout: default
title: "Simulator"
parent:  "Mambolab toolbox"
---

# Simulated Data Generator

The simulated data generator it used to create source signals that are coupled according to a brain state dynamics, in which the brain state can be seen as a particular 
connectivity pattern that remains stable.

The simulated data generator can be found in the `/simulator` folder in the `mambolab` repository, and is the `simulatedata.m` function.

The function needs a `cfg` structure as input, which has the following elements:
   - `cfg.fsample`         : int, the sampling frequency (default = 256)
   - `cfg.LengthTS`        : float, the approximative length of the simulated
                             timeseries (default : 1)
   - `cfg.NumBCS`          : int, number of brain states to be simulated
   - `cfg.RangeLenBCS`     : cell (n_states x 2), range of the length 
                             of brain states occurence (min, max) in sec (default:lengthTS)
   - `cfg.ProbTransMat`    : default uniform distributed transition matrix
   - `cfg.NumParcel`       : number of parcels 
   - `cfg.NumNodesBCS`     : vector (1 x n_states) whose i-th component codes 
                             the number of parcels involved in the i-th BCS
   - `cfg.C`               : adjacency matrix e.g. cfg.C{i}(1,2):1 denotes setting
                             an interaction from parcel 1 to parcel 2 in the
                             i-th BCs
   - `cfg.FreqBandInter`   : vector (2), band in which the frequency-specific
                             interactions occur (in Hz)
   - `cfg.ModelType`       : string, model used to generate data values: 
                            'PhaseDelayed', 'TimeDelayed' or 'AR' 
                            (default:'PhaseDelayed')
   - `cfg.PhaseDelayInter` : cell (n_states x 2), range of the phase delay 
                            of brain states (only for 'PhaseDelayed')
   - `cfg.TimeDelayInter`  : cell (n_states x 2), range of the time delay 
                            of brain states (only for 'TimeDelayed')
   - `cfg.IntARorder`      : int, order of the AR model (only for 'AR')
   - `cfg.SeqBCS`          : timeseries of the BCS occurence (e.g. cfg.SeqBCS:[1 3]
                            means that BCS-1 is the first occurring state,
                            followed by BCS-3)
   - `cfg.LenBCSloc`       : length in seconds of the BCS duration for each
                            occurring state (e.g. cfg.LenBCSloc: [1.5 0.3]
                            means that occurrence of first occuring state 
                            is 1.5 sec, while the one of the second occuring 
                            state is 0.3 sec.

To run the simulator you need to execute `data = simulatedata(cfg)`, and the output will be a FieldTrip compatible structure with the `trial` field that contains the simulated timeseries, while
the `time` field contains the timepoints used and the `cfg` contains the passed parameters.

## Example
The file `examples/example_simulator.m` contains an example for the data generator.
```
cfg                     = [];
cfg.fsample             = 256;  % sampling frequency
cfg.LengthTS            = 20;   % approximative length of the simulated time series (in sec)
cfg.NumBCS              = 4;    % number of brain connectivity states (BCS) to be simulated
cfg.RangeLenBCS         = {[1 2], [0.1 1], [0.1 1], [0.1 1], [0.1 1]}; % range of the length of BCS occurrence (in sec.)

cfg.NumParcel           = 87;   % number of parcels (or channels)
cfg.NumNodesBCS         = randi([2 5], 1, cfg.NumBCS); % number parcels involved in each BCSs

cfg.C                   = {}; % adjacency matrix
```