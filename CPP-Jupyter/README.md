# Obtaining the docker image

## Option 1

```git clone https://github.com/YilengYao/Docker-Jupyter.git```

```cd CPP-Jupyter```

```docker build -t jupyter-cpp .```

```docker run -it -p 8888:8888 jupyter-cpp```

## Option 2

```docker pull yilengyao/jupyter-cpp```

# Mount Docker image to local directory for development

```sudo docker run -it -p 8888:8888 -v <local development directory>:/home/jovyan/work jupyter-cpp```
