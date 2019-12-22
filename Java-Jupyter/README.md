# Special thinks to Spencer Parks for providing the Jupyter Kernel


# Obtaining the docker image

## Option 1
docker build -t jupyter-java .
docker run -it -p 8888:8888 jupyter-java

## Option 2
docker pull yilengyao/jupyter-java

# Mount Docker image to local directory for development

sudo docker run -it -p 8888:8888 -v <local development directory>:/home/jovyan/work jupyter-java