# geosci-course
Resources for running a course using [geosci-labs](https://github.com/lheagy/geosci-labs). 

# why 
[geosci-labs](https://github.com/lheagy/geosci-labs) is a library of notebook-apps for applied geophysics. We hope that they are useful for your courses! 
There are a large number of notebooks in `geosci-labs` and you may only want to use a subset of them to teach your course. 
This repository is intended to help you select the build and deploy a subset of these notebooks for use in your course. 

# scope
There is very little code in this repository; the repository is meant to serve as a template for deploying a course that uses the notebooks in [geosci-labs](https://github.com/lheagy/geosci-labs), though we may one day expand to improving functionality for 
notebooks from other repositories as well. 

The two main components of this repository are: 
- Makefile: command line tools for setting up the repository and keeping it up to date with advancements in [geosci-labs](https://github.com/lheagy/geosci-labs)
- notebooks.yml: structured file for describing which notebooks you want included in your course and where they should be located.

# usage 

## Step 1: create your own fork of this repository 

- First, you will need to [setup a github account](https://github.com/join) if you do not already have one. 
- Then, [fork](https://help.github.com/articles/fork-a-repo/) this repository so that you have your own copy. 

## Step 2: clone and install software requirements

- [Clone](https://help.github.com/articles/cloning-a-repository/) the repository. You can copy the below line and replace `{your-username}` with your github username 
  ```
  git clone https://github.com/{your-username}/geosci-labs
  ```
- change directory into the cloned repository
  ```
  cd geosci-labs
  ```
- install the requirements 
  ```
  make install
  ```

## Step 3: specify the notebooks that you want downloaded

 - edit the file `notebooks.yml` to specify which notebooks you want downloaded and in what directories
 - setup the repository, this downloads the notebooks you specified in `notebooks.yml` 
  ```
  make setup
  ```
  This also downloads an associated environment.yml file which explicitly specifies the exact versions of 
  the direct software dependencies. This ensures that if you distribute your notebooks using [binder.org](https://mybinder.org)
  or use conda environments to manage the software environment that is distributed to students, you can have more confidence
  that upstream changes will not break during the time you are teaching the course. 

## Step 4: tailoring it to your course

- a template notebook, `index.ipynb`, is provided for you and this can serve as a landing-page for your course. 
- once this repository has been set up, you may also want to edit the README so that it is specific to your course

## Step 5: push your changes

- Before committing your notebooks, we recommend running `make clean` in order to clear all output from the notebooks so that they are always archived and deployed in a state that does not include output. 
   ```
   make clean 
   ```
- Then follow [standard git procedure](https://help.github.com/articles/adding-a-file-to-a-repository-using-the-command-line/) to commit and push your notebooks
   ```
   git add .
   git commit -m "commit message"
   git push
   ```

## Step 5.5: updating the code and notebooks

The workflow is opinionated and assumes that you will use the notebooks as-is from [geosci-labs](https://github.com/lheagy/geosci-labs). You are welcome to open issues and create pull requestsin [geosci-labs](https://github.com/lheagy/geosci-labs) to improve them. You are free forge your own path and tailor the notebooks to your course, in which case, you can ignore this section.  

Before updating, make sure that you have committed and pushed any changes. You can always check if you have any uncomitted changes by running
```
make clean
git status
```

If everything is up to date, you can then update the various components of the course.

- The geosci-labs dependencies and the environment.yml will be updated using pypi when you run
  ```
  make update-code
  ```

- If any updates are made to the Makefile, you can fetch them with:
  ```
  make update-makefile
  ```

- To fetch updated notebooks from [geosci-labs](https://github.com/lheagy/geosci-labs), you can run:
  ```
  make update-notebooks
  ```
  Note that this will over-write any changes you have made to the notebooks listed in notebooks.yml. It will not over-write 
  and new notebooks that you have added, nor will it update the index notebook. 

- In order to update the code, makefile and notebooks, you can run 
  ```
  make update-all
  ```

## Step 6: deploy your course
There are several options for deploying your course. Among them, here are a few of the more popular options: 
- [binder.org](https://mybinder.org/) 
- [azure notebooks](https://notebooks.azure.com/)
- If you have a university-supported JupyterHub, then you can request support from the administrator. 
