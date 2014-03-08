## Requirements
 *  [BayeSSC](http://www.stanford.edu/group/hadlylab/ssc/)   
 *  python >= 2.4   


## Example Command lines
The program has several command line options, which can be found using the -h option when executing the script.  Here is a sample execution lines and their explanations:

```  
python hBayeSSC.py --mode initial -i aus_birds_obs -p bss_con_expan.par  -r 1 -t 1000:200000 -u 1 -b ./BayeSSC  
python hBayeSSC.py --mode posterior -i aus_birds_obs -p bss_con_expan.par  -r 1 --uid_list filter.lst  --run_data run_data_iterations_1.csv -u 1 -b ./BayeSSC  
```  

## Options

-p : the par file we will use as a template.  the python script expects the par in a similar format  
-i : the observation file.  This is a tab delimited file, in which the 1st line is a header line.  See the obs_NWHI for the valid headers  
-r : How many times we repeat the execution of BayeSSC for a given model  
-u : a unique identifier.  This can be a string or a number.  It prefixes the index value.  The index is made up of 6 components <uid>_<congruent count>_<total obs>_<trail/repeat #>_<random number with . replaced by _>_<timestamp with . replaced by _>  
-b : the path to where BayeSSC is.  If it isn't supplied, it assumes it is on the Users PATH  
-t : the time Range in which we can randomly select times from.  This is here instead of in the par file, since we now use python to randomly select a time value.  
-m : specify which model to execute.  If -m is not provided, it will execute all models.  
-o : defines where to generate your output.  By default it generates your output in the current working directory  
  
```  
#> python hBayeSSC.py -h

Usage: hBayeSSC.py [options]

Options:
  -h, --help            show this help message and exit
  --mode=MODE           program operation mode [ 'initial', 'posterior' ]
                        [required]
  -p FILE, --par=FILE   par file template [required]
  -i FILE, --obs=FILE   Observation file [required]
  -r NUM, --repeat=NUM  Number of times to try a given congruent group size
                        [required]
  -u UID, --uid=UID     Unique ID to prefix generated indices [required]
  -b PATH, --bayepath=PATH
                        Path to BayeSSC application [default: Located on user
                        PATH]
  --only_hyperstats     When set, will only generate the hyperstats file
  --print_headers       When set will generate a headers.txt and exit
  -o PATH, --outdir=PATH
                        Directory to generate final outputs in (will create
                        missing folders) [default:
                        E:\Source_Files\Work_Related\yvonne]

  Regular Run:
    Options to be applied during mode 'initial'

    -m MODEL, --model=MODEL
                        Run a single model (0 to total entries in observation
                        file) [default: run all models]
    -l TYPE, --LPType=TYPE
                        Loci Rate Priori Type
    -t RANGE, --timerange=RANGE
                        The range of values to select the time from
                        (Integers). Example: 1000:20000  [required]
    --obs_stats         When set, will generate a statistics output for the
                        observation data

  Posterior Run:
    Options to be applied during mode 'posterior'

    --uid_list=FILE     Speccifies a list of UIDs to filter on for Posterior
                        processing [required]
    --run_data=FILE     run data which contains the --uid_list UIDs.  It is
                        used for the Posterior processing [required]
```  