# WifiSignal
Reading and visualizing Wifi signal strength in Linux using Python

STEP 1 – 
Dependencies: install the following python packages using pip
1) numpy
2) pandas
3) jupyterplot
4) seaborn
```
$ pip install numpy pandas jupyterplot seaborn
```

If the sub-dependency package ‘lcurve’ is installed, make sure that the ‘lcurve’ version is 1.1.0
If the version is >1.1.0, revert to the older version using the following commands:
```
$ pip uninstall lrcurve
$ pip install lrcurve==1.1.0
```

STEP 2 – 
Python notebook: WifiSignal.ipynb
You may either download the python notebook and run it on your laptop as you would any python notebook
(OR)
You can directly run the file through [Google Colaboratory](https://colab.research.google.com)
If you do not have experience running python notebooks locally, run it using Google Colab

STEP 3 – 
Create a local connection by following the instructions given here: https://research.google.com/colaboratory/local-runtimes.html

STEP 4 – 
Read the description on the Python notebook cells and run in sequence

## What the code does

Extracting real-time wifi signal strength data in Linux (Ubuntu)

In Linux, the instantaneous Wifi signal strength information is stored in the system file ```/proc/net/wireless```
The contents of the file can be displayed on the terminal using the command
```
> cat /proc/net/wireless
```
One can simply write a bash script to read this data at regular intervals, use an awk command to isolate the strength value and possibly output to a file.
E.g. ```awk 'NR==3' /proc/net/wireless | awk '{ print $4}'```

For plotting continuously it might be easier to use Python, so here are the steps to record and plot signal strength data using Python
1. Read the file using Python and get the signal strength value
- open file
- use `seek` to go to the line with the signal strength data
- use `readline` to read the line, `split` to isolate the strength value
- convert value to float from string\
All this can possibly go into a function which when called returns the power value in dBm.

2. Access time using the time module\
Use a loop to store time and signal strength is an array or data frame

3. Continuous plotting using [ProgressPlot](https://pythonawesome.com/create-real-time-plots-in-jupyter-notebooks/) and regular plot using matplotlib

Errors:
When running the function accessing `ProgressPlot`, the command terminates with the following error message:\
```ValueError: facet_config["plot"]["scale"] must a string```

Resolution:
This error is due to incompatibility of the latest version of the dependency `lcurve`
Uninstall the recent version of `lcurve` and install an older version (1.1.0) using the commands:
```
$ pip uninstall lrcurve
$ pip install lrcurve==1.1.0
```
