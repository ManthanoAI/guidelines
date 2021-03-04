# Jupyter Notebooks

:rocket: to the jupyter and beyond...

- [Rules](#Rules)
- [Basic-setup](#Basic-setup)
- [Virtual-Environment](#Virtual-Environment)
- [Securing-Env-Variables](#Securing-Env-Variables)
- [Docker](#Docker)
- [](#)


## Rules

1. Tell a story for an audience
2. Document the process, not the results
3. Use cell divisions to make steps clear
4. Modularize code
5. Record dependencies (pip -> requirements.txt, conda -> environment.yaml)
6. Use version control
7. Build a pipeline
8. Share and explain your data
9. Design your notebooks to be read, run, and explored
10. Advocate for open research

## Basic-setup

- create an environment (Preferably conda, otherwise virualenv)
- install the needed packages
   `pip install`
- create the requirements file
   `pip freeze > requirements.txt`

## Virtual-Environment

- install <a href="https://docs.conda.io/projects/conda/en/latest/user-guide/install/index.html" rel="nofollow">anaconda</a> or miniconda

- create an environment

   `conda create --name myenv`  

- create an environment with specific python version

   `conda create -n myenv python=3.6`

### Copying Environments to other machines

- export your anaconda environment

   `conda env export > environment.yml`

- recreate it by using

   `conda env create -f environment.yml`

## Securing-Env-Variables

- create an .env file, e.g. `touch .env`

- put your variables in there with your favorite editor, e.g. `nano .env`

   ```bash
   DATABASE_URL=postgres://username:password@localhost:5432/dbname
   AWS_ACCESS_KEY=myaccesskey
   ``` 


- use a package such as `dotenv` to load the env file into notebook

   ```python
   import os
   from dotenv import load_dotenv, find_dotenv
   dotenv_path = find_dotenv()
   load_dotenv(dotenv_path)
   database_url = os.environ.get("DATABASE_URL")
   ```

## Docker

- Principle: `Dockerfile` builds `Image` runs `Container`

### Create a Dockerfile from your existing conda environment

- activate your active conda environment 

   `conda activate YOURENVIRONMENT`

- freeze your packages, create requirements file (use `pip list` instead of `pip freeze`)

   `pip list --format=freeze > requirements.txt`

- create the Dockerfile according to the script below
  - For a miniconda env use: `FROM continuumio/miniconda3:latest`
  - For a anaconda3 env use: `FROM continuumio/anaconda3:latest`
  - instead of using `RUN pip install...` --> `RUN cat...` is used to not break the building process  <b>
  

   ```dockerfile
   FROM continuumio/anaconda3:latest

   COPY requirements.txt /tmp/

   RUN cat /tmp/requirements.txt | xargs -n 1 pip install
   ```

### Run a build of the created Dockerfile

- navigate in the `build context` environment (where the dockerfile os located)
- build the image by running:

   `docker build -t USERNAME/jupyter:TAGNAME .`