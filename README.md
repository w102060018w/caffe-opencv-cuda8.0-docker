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
* [OpenCV 3.3.0](http://opencv.org/)

## Prerequisites

1. Install [Docker](https://docs.docker.com/engine/installation/) on your platform. Here is a [link](https://paper.dropbox.com/doc/Docker-start-WltSz76XRqH7ERWhobmz0) for useful docker command.
2. Install [nvidia-docker](https://github.com/NVIDIA/nvidia-docker), here is a recommand [tutorial](https://github.com/NVIDIA/nvidia-docker/wiki/Installation).

## Setup
### Build Docker images

Download the gpu version images from https://hub.docker.com/r/winnie16/caffe-opencv-cuda8.0/ :
```
docker pull winnie16/caffe-opencv-cuda8.0:gpu
```

### Run the Docker images as Containers

Suppose I plan to use the caffe model on human pose estimation and Nature cut out. <br />
First clone the [Nature-Cut-Out](https://github.com/w102060018w/Nature-Cut-Out) from the github:
```
git clone https://github.com/w102060018w/Nature-Cut-Out.git
```
and then we can run the container with shared filesystems (-v)

```
sudo nvidia-docker run -it -v ~/Nature-Cut-Out:/auto-cutout -p 8888:8888 --expose 6006 --name my-caffe-docker-demo winnie16/caffe-opencv-cuda8.0:gpu bash
```

| Parameter      | Explanation |
|----------------|-------------|
|`nvidia-docker`| This will provision a container with the necessary components to execute code on the GPU. To see more details please take a look at [here](https://devblogs.nvidia.com/parallelforall/nvidia-docker-gpu-server-application-deployment-made-easy/)|
|`-it`             | This creates an interactive terminal you can use to iteract with your container |
|`-v /sharedfolder:/root/sharedfolder/` | This shares the folder `/sharedfolder` on your host machine to `/root/sharedfolder/` inside your container. Any data written to this folder by the container will be persistent. You can modify this to anything of the format `-v /local/shared/folder:/shared/folder/in/container/`. See [Docker container persistence](#docker-container-persistence)
|`-p 8888:8888`   | This exposes the ports inside the container so they can be accessed from the host. The format is `-p <host-port>:<container-port>`. The default iPython Notebook runs on port 8888|
|`--expose 6006` | Expose a port or a range of ports inside the container|
|`--name my-caffe-docker-demo`| You can assign a name to the container|
|`winnie16/caffe-opencv-cuda8.0:gpu`   | This is the image you are going to run. The format is `image:tag`|
|`bash`       | This provides the default command when the container is started. Even if this was not provided, bash is the default command and just starts a Bash session.|

### Using Jupyter Notebook

Type the following command inside the container and go to the [localhost:8888](http://localhost:8888/) you can see the jupyter notebook start running.

```
jupyter-notebook --ip=0.0.0.0 --allow-root
```

If you run Docker on the GCP, you need to connect your local host to the port running on the GCP, please follow this [link](https://paper.dropbox.com/doc/Running-Jupyter-Notebook-on-the-GCP-SoWlQwj2xpgaR9k2AhH3Z).


## Acknowledgments

Big thanks to 
* [dl-docker](https://github.com/floydhub/dl-docker)
* https://github.com/jerryrt/docker_ubuntu_14.04-opencv-git-latest <br />
I mainly modify the Dockerfile from the above two resources.

