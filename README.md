### [Introduction](https://github.com/afif-fauzan/gee-atmcorr-S2#inroduction) | [Installation and Usage on Jupyter Notebook](https://github.com/afif-fauzan/gee-atmcorr-S2#installation) | [Usage on Kaggle](https://github.com/afif-fauzan/gee-atmcorr-S2#usage-on-kaggle)
____
### Notes from the [author](https://github.com/samsammurphy/gee-atmcorr-S2)
> ### !
> ### This repo is no longer under development
> and is probably broken given the pace of the Google Earth Engine team. I am now the CEO of [Earthscope](https://earthscope.io), > a startup company from [Entrepreneur First](https://joinef.com), so have no time to squash any bugs that I introduced (sorry) or > that have since appeared...
> The rest of the repo is 'as was', use at your own peril.
____




### Introduction

Atmospheric correction of Sentinel 2 imagery in Google Earth Engine using [Py6S](http://py6s.readthedocs.io/en/latest/). Runnable on Jupyter Notebook and Kaggle. Doesn't work on Google Collab. If you wish to run it on Kaggle, jump to [Usage on Kaggle](https://github.com/afif-fauzan/gee-atmcorr-S2#usage-on-kaggle).

### Installation

#### Recommended: Docker

The following [docker](https://www.docker.com/community-edition) container has all dependencies to run the code in this repository

`docker pull samsammurphy/ee-python3-jupyter-atmcorr:v1.0`

You can also build a docker container from scratch using this [Dockerfile](https://github.com/gee-community/ee-jupyter-contrib/tree/master/docker/atmcorr-ee) from the [gee-community](https://github.com/gee-community) repo.

#### Alternative: Manual installation

This repo has the following prerequisites

- [Python 3.x](https://www.python.org/downloads/)
- [Google Earth Engine Python API](https://developers.google.com/earth-engine/python_install_manual)
- [Jupyter](http://jupyter.readthedocs.io/en/latest/install.html)
- [Py6S](http://py6s.readthedocs.io/en/latest/installation.html)

### Usage

To run the docker container with access to a web browser

`$ docker run -i -t -p 8888:8888 samsammurphy/ee-python3-jupyter-atmcorr:v1.0`

Once inside the container, authenticate Earth Engine

`earthengine authenticate`

then grab the source code for this repo

`git clone https://github.com/samsammurphy/gee-atmcorr-S2`

and run the example jupyter notebook

```
cd gee-atmcorr-S2/jupyer_notebooks/
jupyter-notebook sentinel2_atmospheric_correction.ipynb --ip='*' --port=8888 --allow-root
```

this will print out a URL that you can copy/paste into your web browser to run the code.

If the URL is *http://(something_in_parentheses)* then you will need to change the parentheses and its contents for *localhost*. A valid URL should look something like..

http://localhost:8888/?token=...

### Saving authentication

After authenticating with `earthengine` and cloning the repository you can save the changes
you've made to the container with `docker commit`. Docker commit will create a new image from
a running containers current state.

With the container still running, open a new terminal to get the container's ID:

`docker ps`

copy the ID to clipboard and run

`docker commit [ID] gee-atmcorr-s2:myauth`

to commit the image. Now if you run

`docker images`

your newly committed image should be at the top of the list.

You can now start the note book with

```
docker run -i -t -p 8888:8888 gee-atmcorr-s2:myauth

jupyter-notebook /gee-atmcorr-S2/jupyer_notebooks/sentinel2_atmospheric_correction.ipynb --ip='*' --port=8888 --allow-root
```

### Usage on Kaggle

If you don't have Python or Jupyter Notebook installed on your computer, you can use online notebook such as Kaggle (Google Collab wouldn't work, unfortunately), which can be accessed [here](https://www.kaggle.com/fifauzan/sentinel2-atmospheric-correction-py6s/edit/run/38660519).

Prior to running the code, you should enable the internet on the notebook settings. You should also logged in to the google account linked with Google Earth Engine since it would use the GEE API.

![kaggle](https://github.com/afif-fauzan/gee-atmcorr-S2/blob/master/kaggle.jpg?raw=true)

The process should took less than five minutes. Once it done, you could access the corrected image on your Earth Engine asset.

![result](https://github.com/afif-fauzan/gee-atmcorr-S2/blob/master/gee-result.jpg?raw=true)
![result2](https://media.giphy.com/media/jVMrWzJclLZswVBte4/giphy.gif)
