# Bayeslands Workshop

*Part of the badlands (Basin and Landscape Dynamics) suite* from the The University of Sydney  

These materials are designed to give you a brief introduction to the BADLANDS (Basin and Landscape Dynamics) modelling code, extended functionality provided by pyBadlands, the Bayesian inference methods in Bayeslands, and additional helper tools. 
See https://github.com/badlands-model/ and the repositories therin for details on various Badlands/Bayeslands incantations.

[Email us](mailto:nathaniel.butterworth@sydney.edu.au)


## Installation

This repo is at http://github.com/badlands-model/Bayeslands-Workshop


### Via Docker

The easiest way to install and run the **Bayeslands Workshop** is by downloading through Docker.

Download the [dockerfile](Docker_details/Dockerfile) 

Change into the folder with the docker file, then execute:

``` 
docker build -t bayeslands . 
```

Then to run, execute:

```
docker run -p 8888:8888 bayeslands
```

From there you can navigate this folder structure within the Jupyter notebook environment from your web browser.


### Via Compile

Or download the repo and compile pyBadlands.

```
git clone https://github.com/badlands-model/Bayeslands_Workshop.git
cd Bayeslands_Workshop/pyBadlands/libUtils
make 
cd -
pip install -e Bayeslands_Workshop
```
Then launch the [StartHere.ipynb](StartHere.ipynb) notebook, that resembles the readme file you are reading now!

#### Dependecies for compiliation

If you compile this workshop locally, then several dependencies (easily installed with anaconda and pip) are required. These steps should get you an evironment ready to compile pyBadlands (above).

```
conda create --name pybad python=2.7.13 
source activate pybad
conda install jupyter h5py markupsafe numba=0.35.0 singledispatch backports_abc certifi jsonschema ipyparallel
conda install path.py matplotlib=2.0.2 pandas scipy=0.19.1 basemap=1.0.7 mpi4py plotly  Cython==0.20 
conda install PIL  
pip install ez_setup colorlover cmocean scikit-fuzzy pyevtk zmq git+https://github.com/badlands-model/triangle

git clone https://github.com/awickert/gFlex.git 
cd gFlex/
python setup.py install
cd ..
```


## Workshop

Following the notebooks in order will guide you through understanding how the Badlands and Bayeslands models are built and executed. Hopefully you should be able to replace these example datasets with your own workflows.


### Pre-processing

The pre-processing notebooks will help you to create surface grids for generic, real (based on etopo1) topographic/bathymetric datasets.

* [Generic Surface](Examples/topoCreate.ipynb): generic surface generation notebook.
* [etopo1 Surface](Examples/etopoGen.ipynb): etopo1 surface generation notebook.
* [Bayeslands Surface](Examples/bl_topogenr.ipynb): surface to run and test models against.


### Running Badlands and Bayeslands

We provide a full examples that create a surface and then runs multiple simulations to estimate uncertainties in your parameter selections.

* [Badlands Mountain Example](Examples/mountain.ipynb): running a standard Badlands model.
* [Bayeslands Crater Example](Examples/bl_mcmc.ipynb): surface to run and test models against.
* [PT Bayeslands Crater Example](Examples/ptBayeslands.ipynb): surface to run and test models against using parallel tempering.

 
 
### Post-processing

Many post processing analysis steps can be done to produce various figures and interrogate different parts of the numerical model.

* [Likelihood surface creation](Examples/bl_surflikl.ipynb): explores the the parameter space in evaluating the model.


# Additional notes

## Badlands, Bayeslands, What?

**Badlands** is the code (originally written in Fortran) to model surface processes.

**pyBadlands** was an extension to Badlands that allowed for easy manipulation of model parameters, input files, execution, etc via the Python programming language.

**Bayeslands** uses pyBadlands and applies Bayesian inference to the Badlands models to essentially provide estimates of error. It runs 1000's of Badlands models with slightly different parameter choices, and compares the results against a 'known' solution to estimate an error. There are different versions of Bayeslands being developed that use different techniques (paralleltempering, surrogate assissted) to optimise accuracy and exploration efficiency in the models with different trade-offs.


## Jupyter in a nutshell


### What is this ?

This is an example of the iPython / Jupyter notebook system. They are a form of literate programming in which we can mix textbook instruction and explanations with code (in this case, python) that can also be run and edited. The text and mathematics in the notebooks requires a little preliminary learning. 

**Note:**
*The docker containers will not save your information when you will refresh the notebooks. So the content that you will create is ephemeral: it will disappear with the container if you do not capture the output by mounting the volume or copying the data to your local machine. Therefore it is better to attach a volume to the docker image. You can do that using the **Kitematic** interface and selecting a folder where you will store your own notebooks as well as your Badlands input and output files.*

*The docker containers system settings are configurable in the [VirtualBox](http://www.virtualbox.org) which is running in the background of each docker image. For example, you can change the Base Memory and the Number of Processors associated to the vm.*


### Markdown

You can document your iPython notebooks by making some cells into **Markdown** cells. Markdown is a way of formatting text that is supposed to be almost as readable un-rendered as when it is tidied up. You might argue that it looks equally bad either way, but that's tough because the notebooks use it and that's how I want you to produce nice looking output to hand in as an assignment !

If you look at the **Markdown** cells as source code (by double-clicking on them) you will see how the raw text looks. To get back to the pretty version of the text, hit shift-enter.

### Maths

In a browser, you can render equations using a javascript tool called **Mathjax** which is build into the iPython notebooks. 

You can build in symbols to your text such as $\pi$ and $\epsilon$ if you use the \$ signs to indicate where your equations begin and end, and you know enough $\LaTeX$ [try it here !](http://www.codecogs.com/latex/eqneditor.php) to get by.

Equations in `display` mode are written like this (again look at the source for this cell to see what is used)

\\[ e^{i\pi} + 1 = 0 \\]

or even like this

\begin{equation}
%%
    \nabla^4 \psi = \frac{\partial T}{\partial x}
%%    
\end{equation}

Go back to the rendered form of the cell by 'running' it.

### Links 

[Markdown Website](http://daringfireball.net/projects/markdown/)  
[Mathjax Website](http://docs.mathjax.org)  
[Jupyter Notebooks](http://www.jupyter.org)
