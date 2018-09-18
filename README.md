# toy_notebooks

Ken's resource model is notebookized and extended. The main entry point is 

resource_runner.ipynb

which imports a number of components and makes plots and tables. It should work to import this github repository, and run this notebook. 

This notebook is mostly driven by json inputs. (in the json subdirectory). They are hierarchical to allow us to easily track when changes were made where in the parameters themselves. We will soon outgrow this as being too complicated, but not quite yet.

the actual spot where the json files are read in is

```
jsons=['json/RelyOnMiniAOD.json', 'json/Analysis.json', 'json/2018changes.json', 'json/IntroduceNanoAOD.json'] 
```

which shows the order in which json files are read and dictionaries revised. Eg, IntroduceNanoAOD.json can (and does) overwrite parameters in the previous json file inputs.

The main model components are:
 - CPU (resource_cpu.ipynb)
 - Disk and tape (resource_disktape.ipynb)
 - Cost (under construction, CostEvolution.ipynb)
 
 
 Unfortunately there is only a minimal link between the CPU model and the disk/tape model. These do share
 input parameters, but sometimes get out of sync due to things hardwired in the code itself.
 
 The main components of the model are:
 - Workflow types: Data, LHC Monte Carlo, HLLHC Monte Carlo. These are basically hardwired in
 - Evolution in software performance (eg, improvement made each year for each type of workflow)
 - Model for prompt and rerecos - also hardwired in. This we need to change.. (eg, to add a fraction of data that must be prompt recoed
 - Analysis model: CPU and disk (the latter being quite made up) needs based on the current "analysis set" (relevant years of data taking)
 - Replica model for data on disk and tape (including deletion policies)
 - Disk space for operations / staging space
 - metrics : I started to define metrics that could be used to evaluate changes as being "good" or "bad" based on some simple things. Cost of the computing during the HL-LHC startup is one example
