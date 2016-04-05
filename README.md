## docker file

docker file for mxnet and ipython

### Usage for Dockerfile

1. copy Dockerfile to an empty folder

2. build image
```bash
docker build -t=HunterXu/mxnet_jupyter .
```

3. run this docker image , mapping current folder to /root/workspace in the docker container

```bash
docker run --rm -it -p 8888:8888 -v "$(pwd):/root/workspace" HunterXu/mxnet_jupyter
```

4. visit http://127.0.0.1:8888

### Usage for mk_dev.sh

mk_dev.sh can generate /dev/nvidiactl /dev/nvidia-uvm /dev/nvidia0
