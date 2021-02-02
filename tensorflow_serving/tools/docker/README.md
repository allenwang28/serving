Files for using the [Docker](http://www.docker.com) container system.
Please see [Docker instructions](https://github.com/tensorflow/serving/blob/master/tensorflow_serving/g3doc/docker.md)
for more info.

## Commands to build TF serving on TPU VM:
Note: TPU VM is not yet widely available. This must be run on a TPU VM.

```
# Optional env names for consistency.
export CONTAINER_NAME=tf_serve
export IMAGE_NAME=$USER/tensorflow-serving-tpu
export MODEL_PATH=/path/to/my/model

# Build the Dockerfile with /bin/bash entrypoint
docker build --pull -t $IMAGE_NAME -f Dockerfile.tpu .

docker run -it -p 8501:8501 --name $CONTAINER_NAME --privileged  -v "/lib/:/lib/" -v "$MODEL_PATH/:/models/model" $IMAGE_NAME &
```

To run in dev mode (`/bin/bash` entrypoint):
```
export IMAGE_NAME=$USER/tensorflow-serving-devel
docker build --pull -t $IMAGE_NAME -f Dockerfile.devel-tpu .

docker run -it -p 8501:8501 --name $CONTAINER_NAME --privileged  -v "/lib/:/lib/" -v "$MODEL_PATH/:/models/model" $IMAGE_NAME

```
