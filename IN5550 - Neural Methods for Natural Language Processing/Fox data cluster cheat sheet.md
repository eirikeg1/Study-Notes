
# Connecting to fox
---
### Outside Fox Shell

* Connect to Fox: ```ssh -X ec-eirikeg@4228ouD#28422502```
	* .zshrc alias: ```fox```

### Inside Fox Shell

* Change login after connection: ```ssh login2```
* Project directory path: ```/fp/projects01/ec30```
	* Alias: ```ec30```
	* Alias for ```ec30/IN5550```: `IN5550`
	

# Modules
---

* When loading modules the environmental variables are changed

### Commands

* In order to load all modules use alias: ```load_modules```
* Load module: ```module load <module-name>```
* Unload modules: ```module purge```
* Use _ec30_ modules directory: ```module use -a /fp/projects01/ec30/software/easybuild/modules/all/```
* 
* Check available modules: ```module avail```
* Check loaded modules: ```module list```
* Check available versions of modules: ```module spider <search-keyword>```


# Compute-jobs

1. Create a `.slurm` script, follow the [template](https://github.uio.no/in5550/2024/blob/main/sample.slurm) from github
2. Run job with `sbatch <filename-with-ending`
3. 
