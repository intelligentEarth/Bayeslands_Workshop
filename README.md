# Bayeslands Workshop

*Part of the badlands (Basin & landscape dynamics) suite* from the The University of Sydney  

These materials are designed to give you a brief introduction to the BADLANDS (Basin and Landscape Dynamics) modelling code, extended functionality provided by pyBadlands, the Bayesian inference methods in Bayeslands, and additional helper tools. 
See https://github.com/badlands-model/pyBadlands and the repositories therin for details on various Badlands/Bayelands incantations.

[email us](mailto:tristan.salles@sydney.edu.au)


## Installation

This repo is at http://github.com/badlands-model/Bayeslands-Workshop


### Via Docker

The easiest way to install and run the **Bayeslands Workshop** is by downloading through Docker.

Download the [dockerfile](/Bayeslands_Workshop/Docker_details/Dockerfile) 

Change into the folder with the docker file, then execute:

``` 
docker build -t bayeslands . 
```

Then to run, excute:

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
pip install -e /build/Bayeslands_Workshop
```



## Workshop

Following the notebooks in order will guide you through understanding how the Badlands and Bayeslands models are built and executed. Hopefully you should be able to replace these example datasets with your own workflows.


### Pre-processing

The pre-processing notebooks will help you to create surface grids for generic, real (based on etopo1) topographic/bathymetric datasets.

* [Generic Surface](/Bayeslands_Workshop/Examples/topoCreate.ipynb): generic surface generation notebook.
* [etopo1 Surface](/Bayeslands_Workshop/Examples/etopoGen.ipynb): etopo1 surface generation notebook.
* [Bayeslands Surface](/Bayeslands_Workshop/Examples/bl_topogenr.ipynb): surface to run and test models against.


### Running Badlands and Bayeslands

We provide a full examples that create a surface and then runs multiple simulations to estimate uncertainties in your parameter selections.

* [Bayeslands Crater Example](/Bayeslands_Workshop/Examples/bl_mcmc.ipynb): surface to run and test models against.
* [PT Bayeslands Crater Example](/Bayeslands_Workshop/Examples/ptBayeslands.ipynb): surface to run and test models against using parallel tempering.

 
 
### Post-processing

Many post processing analysis steps can be done to produce various figures and interrogate different parts of the numerical model.

* [Likelihood surface creation](/Bayeslands_Workshop/Examples/bl_surflikl.ipynb): explores the the parameter space in evaluating the model.


# Additional notes

## Badlands, Bayeslands, What?

**Badlands** is the code (originally written in Fortran) to model surface processes.

**pyBadlands** was an extension to Badlands that allowed for easy manipulation of model parameters, input files, execution, etc via the Python programming language.

**Bayeslands** uses pyBadlands and applies Bayesian inference to the Badlands models to essentially provide estimates of error. It runs 1000's of Badlands models with slightly different parameter choices, and compares the results against a 'known' solution to estimate an error.


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