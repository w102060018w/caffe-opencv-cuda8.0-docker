## Docker image for caffe

Here is the dockerfile to run with caffe and other common libraries.

## Details

When building the images with the provided Dockerfile, you will get:

* Ubuntu 14.04
* [Caffe](http://caffe.berkeleyvision.org/)
* [CUDA 8.0](https://developer.nvidia.com/cuda-toolkit) (GPU version only)
* [cuDNN v5](https://developer.nvidia.com/cudnn) (GPU version only)
* [iPython/Jupyter Notebook](http://jupyter.org/)
* [Numpy](http://www.numpy.org/), [SciPy](https://www.scipy.org/), [Pandas](http://pandas.pydata.org/), [Scikit Learn](http://scikit-learn.org/), [Matplotlib](http://matplotlib.org/)
* [OpenCV](http://opencv.org/)

## Prerequisites

1. Install [Docker](https://docs.docker.com/engine/installation/) on your platform. Here is a [link](https://paper.dropbox.com/doc/Docker-start-WltSz76XRqH7ERWhobmz0) for useful docker command.
2. Install [nvidia-docker](https://github.com/NVIDIA/nvidia-docker), here is a recommand [tutorial](https://github.com/NVIDIA/nvidia-docker/wiki/Installation).

## Build Docker images

Download the gpu version images from https://hub.docker.com/r/winnie16/caffe-opencv-cuda8.0/ :
```
docker pull winnie16/caffe-opencv-cuda8.0:gpu
```

## Run the Docker images as Containers

```
sudo nvidia-docker run -it -v ~/Realtime_Multi-Person_Pose_Estimation:/HPE_model_testing_0725 -p 8888:8888 --expose 6006 --name my-caffe-docker-demo winnie16/caffe-opencv-cuda8.0:gpu bash
```

## Using Jupyter Notebook

```
jupyter-notebook --ip=0.0.0.0 --allow-root
```
go to the [localhost:8888](http://localhost:8888/) you can see the jupyter notebook start running. <br />
If you run Docker on the GCP, you need to connect your local host to the port running on the GCP, please follow this [link](https://paper.dropbox.com/doc/Running-Jupyter-Notebook-on-the-GCP-SoWlQwj2xpgaR9k2AhH3Z).


## Acknowledgments

Big thanks to 
* [dl-docker](https://github.com/floydhub/dl-docker)
* https://github.com/jerryrt/docker_ubuntu_14.04-opencv-git-latest <br />
I mainly modify the Dockerfile from the above two resources.
