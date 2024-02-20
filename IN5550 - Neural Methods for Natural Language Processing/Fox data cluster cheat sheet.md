_University of Oslo high performance GPU cluster_
# Connecting to fox
---
### Outside Fox Shell

* Connect to Fox: ```ssh -X ec-eirikeg@fox.educloud.no```
	* .zshrc alias: ```fox```
* [Fox connection guide](https://www.uio.no/studier/emner/matnat/ifi/IN5550/v24/setup.html)
* [Online fox notebook](https://ondemand.educloud.no/pun/sys/dashboard/batch_connect/sessions)

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
* Use _ec30_ modules directory: 

```Bash
module use -a /fp/projects01/ec30/software/easybuild/modules/all/
```
* 
* Check available modules: ```module avail```
* Check loaded modules: ```module list```
* Check available versions of modules: ```module spider <search-keyword>```


### Specific modules

* **Gensim format** (format for storing model data in NumPy arrays): 
```Bash
	module load nlpl-gensim/4.3.2-foss-2022b-Python-3.10.8
```


# Compute-jobs

1. Create a `.slurm` script, follow the [template](https://github.uio.no/in5550/2024/blob/main/sample.slurm) from github
2. Run job with `sbatch <filename-with-ending`
3. 

