# Python_Profiling

Combines the outputs of profiling packages: line_profiler and memory_profiler into one plot, with annotations for function locations.

## Files
`profiling_examples.ipynb` -- demonstrates functionality by showing the output plots from two Python scripts

`profile_processing.py` -- Contains the Python class that processes the profiling results

`create_profiles.sh` -- bash script that runs memory_profiler, line_profiler, and the profile processing all at once

`/scripts_to_profile/modified_Lorenz.py` -- Script that integrates a modified (3-"lobes") Lorenz ODE system, & plots the trajectory using Plotly.

`/scripts_to_profile/profiler_testing.py` -- Script that does some arbitrary NumPy operations
  
profiles (`.txt` and `.lprof`) -- Contains the results of the profiling

## Run in steps

Can work in UNIX or Windows PowerShell. 

1: Run the memory profiler, and save the output in a text file

```bash
python -m memory_profiler "/path/to/python/script.py" > "your_memory_profile_name.txt"
```

2:  Run the line profiler to generate the the lprof file

```bash
kernprof -l "path/to/python/script.py"
```

3: Run line profiler with python, and save output in a text file

```bash
python -m line_profiler "/path/to/lprof/script.py.lprof" > "your_line_profile_name.txt"
```

4: Use the ProfileProcessor() to plot the results
```bash
export lpath="/path/to/your_line_profile_name.txt"
export mpath="/path/to/your_memory_profile_name.txt"
python profile_processing $mpath $lpath
```

## Run all at once

Only works on UNIX. Run the following (without the .py file extension appended to "python_script"). This assumes the script is located in /scripts_to_profile/

```bash
pythonFile="python_script" bash create_profiles.sh
```
