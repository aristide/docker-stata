# ⚠️ Disclaimer

This is an unofficial repository to run Stata using Docker. You must have the license code. Otherwise, you can't execute Stata both on batch mode or via Jupyter because the `stata.lic` file is not attached in the Docker images.

Forked from [ledwindra repository](https://github.com/ledwindra/docker-stata)

# Prerequisites

This image will work with Stata version 17+ and higher cause the backbone of running Stata on Jupyter is [`nbstata`](https://github.com/hugetim/nbstata) library.

# Usage

You can build the image locally on your own. First, you must have Stata (version 17+) installer in `.tar.gz` format and save it in this directory `(./jupyter-stata/)`

```bash
# build image locally
docker build -t jupyterlab-stata:18 .

# run image
# run this command if you don't have stata.lic file 
docker run -p 8888:8888 --name=jupyter-stata jupyterlab-stata:18
# or run this command line if you have the stata.lic file in the current location
docker run -p 8888:8888 -v  ${PWD}/stata.lic:/usr/local/stata/stata.lic --name=jupyterlab-stata jupyterlab-stata:18

# stop container
docker stop jupyterlab-stata

# remove container if no longer needed
docker rm jupyterlab-stata
```

To run Stata, you need to create `stata.lic` file inside `/usr/local/stata/` directory. Otherwise, you will get the following error message when you prompt Stata batch mode:

```
Cannot find license file
stata.lic
```

By default, I install `vim` and `nano` text editor. So type the following command `vim /usr/local/stata/stata.lic` and paste the following values:

```
SERIAL!AUTHORIZATION!CODE!FIRST NAME!LAST NAME!FOUR DIGITS FROM LICENSE!
```

# Jupyter

It assumes that your default stata edition is `MP`. If you use Stata `IC` or `SE`, you need to change its configuration file by typing `vim ~/.nbstata.conf`:
- Find `stata_dir` and replace its value to `/usr/local/stata`. 
- Find `edition` and replace its value tp to `mp` or `se`.

# How it works

Demo1

![demo1](img/demo1.gif)

Demo2

![demo2](img/demo2.gif)
