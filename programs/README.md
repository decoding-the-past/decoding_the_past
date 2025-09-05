# Installation manual
For this **Decoding The Past** course we need the programs Python, R, and Tracer. This tutorial shows how to install them and the required add-on packages.

## 1. Install python 3.12

https://www.python.org/downloads/release/python-3129/

Direct download links:

[Windows x86](https://www.python.org/ftp/python/3.12.9/python-3.12.9-amd64.exe)

[Mac](https://www.python.org/ftp/python/3.12.9/python-3.12.9-macos11.pkg)

[Linux](https://www.python.org/ftp/python/3.12.9/Python-3.12.9.tgz)


This installation has not been tested on machines using ARM CPUs like Chromebooks or Windows and Linux using Qualcomm/Snapdragon chips.


If you are using Windows, make sure to check the two boxes `Install launcher` and `Add python to PATH`

<img src="https://github.com/decoding-the-past/decoding_the_past/blob/main/figures/python_path.png" alt="Check boxes" width="750">

## 2. Install R

Download and install [R](https://cran.rstudio.com/)

If you are using Windows, you need to manually add the command line version of R (called _Rscript.exe_) onto your PATH system variables. You can find some instructions [here](https://www.java.com/en/download/help/path.html)

- Press Windows + R keys
- Type _sysdm.cpl_ to open the control panel
- Click on the _Advanced_ tab
- Click on _environmental variables_
- Click on the entry _PATH_ in the field _System variable_ and then _Edit..._
- Click on the button _New_ and add the path to the bin folder of your R installation, e.g. ```C:\Program Files\R\R-4.45.1\bin```
- Move this entry up to no be in the last position

This is a good moment to verify that python has been added to the system PATH during its installation. Check if the PATH includes the directory of your python, e.g. ```C:\Program Files\python312\``` and ```C:\Program Files\python312\Scripts\```.

<img src="https://github.com/decoding-the-past/decoding_the_past/blob/main/figures/rscript.png" alt="system path" width="750">

RStudio is recommended for the DeepDive tutorial but not an requirement. You can install it from [here](https://posit.co/downloads/).


## 3. Obtain Tracer

The program Tracer is used to assess convergence of Bayesian inferences by opening a `log` file of an analyses. You can download it from [here](https://github.com/beast-dev/tracer/releases). Tracer is an executable file that can just be opened and no installation is needed.

## 4. Download the course repository

- Follow this [link](https://github.com/decoding-the-past/decoding_the_past/archive/refs/heads/main.zip) to download this tutorial's repository.
- Unzip the compressed file (`decoding_the_past-main.zip`) if not automatically done by your browser and rename it `decoding_the_past`.
  You can move the `decoding_the_past` folder in your preferred working direcotry. 
- Open your command prompt window on Windows or a terminal console on Mac/Linux and move with `cd` into the unzipped downloaded folder
	- You need to use backslashes on Windows, e.g.

		```
		cd c:\...\decoding_the_past
		```

		and slashes on Mac and Linux

		```
		cd /.../decoding_the_past
		```



## 5. Create a virtual python environment

- Create a virtual environment called `venv` within your `decoding_the_past` folder. Sometimes Windows requires ```py``` instead of ```python```. **Note:** if you had previous versions of Python installed on your machine (especially on a Mac) you may have to type `python3.12` instead of just `python` to make sure the virtual environment is created using the latest version. 
	
	```
	python -m venv venv
	```

- Activate the virtual environment

	- Windows

		```
		.\venv\Scripts\activate
		```
	- Mac and Linux
	
		```
		source venv/bin/activate
		```

- Check your Python version by typing:
  ```
  python
  ```
  This should print something like:
  ```
Python 3.12.3 [...]
Type "help", "copyright", "credits" or "license" for more information.
>>> 
  ```
- quit python before going to the next step:
```
quit()
```


## 6. Install python packages

Install all the packages listed in the `requirements.txt` file located in the subdirectory `programs` of your `decoding_the_past` folder

Windows:
```
pip install -r .\programs\requirements.txt
```

Mac/Linux:
```
pip install -r ./programs/requirements.txt
```

## 7. Install R packages

Open R and install the packages we need.

```
install.packages(c("remotes", "vioplot", "scales"))
library(remotes)
remotes::install_github("DeepDive-project/DeepDiveR")
q()
```

## 8. Check installation

As the last step, you can use this python script to verify that all installations were successful.

Windows:
```
python .\programs\test_programs.py
```

Mac/Linux:
```
python ./programs/test_programs.py
```

<img src="https://github.com/decoding-the-past/decoding_the_past/blob/main/figures/test_cpeg_programs.png" alt="test installations" width="500">
