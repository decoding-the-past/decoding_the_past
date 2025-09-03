# Clade age estimation using a Bayesian Brownian Bridge


The BBB models implemented in this program are described in Silvestro et al. 2021 [Nature Ecology and Evolution](https://doi.org/10.1038/s41559-020-01387-8) and Carlisle et al. 2023 [Current Biology](https://doi.org/10.1016/j.cub.2023.06.016). 

## Running rootBBB
The BBB model requires two sources of information: a diversity count through time based on predefined bins (e.g. of 1 myr) and a modern diversity count. The latter indicates the approximate number of known living species of a clade. If the clade is extinct the number can be set to 0. The BBB model uses Bayesian inference with data augmentation to infer 1) an approximate preservation rate, 2) the clade age, and 3) the extinction time, where applicable. The model works even for clades with very limited fossil record, where e.g. a [PyRate](https://github.com/dsilvestro/PyRate) analysis would not work. 

### Navigate to your `decoding_the_past` repository and activate the virtual environment
The PyRate inference will be performed in your command window or terminal and makes use of your virtual environment. Move into your `decoding_the_past` repository and activate the virtual environment.

* Windows
 
    ```
    cd c:\...\ decoding_the_past
    .\venv\Scripts\activate
    ```

* Mac and Linux

    ```
    cd /.../decoding_the_past
    source venv/bin/activate
    ```


### Running on simulated data
You can test the BBB model on simulated data using the `-sim` command to specify how many simulations you want to run. 
For instance you can use:

```
python rootBBB.py -sim 10 -seed 9600
```

This command will sequentially simulate and analyze 10 datasets (the argument `seed` fixes the random generator to create reproducible results. The output files are saved in the same directory as the program and include:  
1. a plot of the simulated trajectory  
2. a log file with the posterior samples  
3. a text file with the summary of true and estimated parameters across all simulations.

The sampled parameter values are saved in the `*.log` file, which can be inspected in the program [Tracer](https://beast.community/tracer).

To simulate an extinct clade you can add the `-sim_extinct 1` commmand:

```
python rootBBB.py -sim 10 -seed 9600 -sim_extinct 1
```
The simulated dataset(s) will be analyzed using the MCMC algorithm implemented in the program. You can specify the number of iterations, sampling frequency and print frequency using the `-n`, `-s`, and `-p` commands, respectively (default: `-n 25000 -s 100 -p 1000`). 

**The BBB model includes two flavors of preservation models** with constant or time-increasing rate. To run the analysis using the latter you can use the `-q_var 1` setting: 

```
python rootBBB.py -sim 10 -seed 9600 -q_var 1
```

The model uses a uniform prior on clade age and the upper boundary must be specified. This is done using the `-max_age` command (default value = 300. 


### Running on empirical data

**Angiosperm fossil record**

The file `family_diversity.txt` includes a list of angiosperm families and they modern species richness(based on [Silvestro et al. 2021](https://doi.org/10.1038/s41559-020-01387-8)). The `fossil_counts*.txt` files include counts of number of species sampled for each family in time bins of 2.5, Myr.  

**Mammal fossil record**
The file `mammal_modern_species.txt` includes a list of mammalian families and they modern species richness (from [Carlisle et al. 2023](https://doi.org/10.1016/j.cub.2023.06.016)). The `mammal_data_binned.txt` file includes counts of number of species sampled for each family in time bins of 1 Myr.  


**Examples**

To run an analysis on an empirical data you should provide two input files, both tab separated tables. The first one includes binned fossil counts for one or more clades with the first column specifying the age of the bins and the following columns providing fossil counts for each clade. Clade names are provided as the header of the table. 
Time bins with no fossil occurrences of a clade will be set to zero. 

The second file provides the clade modern diversity, set to 0 for extinct clades. The table includes two columns with clade names (matching those in the fossil count table) and clade modern diversity. 


This is an example of an analysis of an extant plant clade:

```
python rootBBB.py -fossil_data .../bbb_analysis/fossil_counts_2.5.txt -div_table .../bbb_analysis/family_diversity.txt -q_var 1 -clade_name acanthaceae
```

where `...` should be replaced by the full path to your files. 
This is an example with an extinct mammal clade:

```
python rootBBB.py -fossil_data .../bbb_analysis/mammal_data_binned.txt -div_table .../bbb_analysis/mammal_modern_species.txt -clade_name Amphicyonidae
```

