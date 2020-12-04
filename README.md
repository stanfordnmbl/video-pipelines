# Human pose estimation algorithms easy to use

## Requirements

* Windows/MacOS/Linux
* [Git client](https://git-scm.com/downloads)
* [Docker client](https://www.docker.com/products/docker-desktop)
* Optional: [NVIDIA docker](https://github.com/NVIDIA/nvidia-docker) for GPU support (10x faster processing)

## OpenPose

Create a directory (say `data` as in the example below) and put your video (e.g. `video.mp4`) in that directory.

For CPU processing of your video run:
```
docker run -v $(pwd)/data:/openpose/data stanfordnmbl/openpose-cpu\
  /openpose/build/examples/openpose/openpose.bin\
  --video /openpose/data/video.mp4\
  --display 0\
  --write_json /openpose/data/keypoints\
  --render_pose 0
```
Note that CPU processing is very slow -- it'll take at least 15x the duration of the video to process.

For GPU processing of your video run:
```
docker run --gpus=1 -v $(pwd)/data:/openpose/data stanfordnmbl/openpose-gpu\
  /openpose/build/examples/openpose/openpose.bin\
  --video /openpose/data/video.mp4\
  --display 0\
  --write_json /openpose/data/keypoints\
  --render_pose 0
```

Resultis will be store in `data/keypoints` directory.

In the scripts above `$(pwd)/data` corresponds to the path in which your `data` directory is stored.

## License

In this repository we only provide instructions on how to run software. Corresponding licenses apply.
See [OpenPose repository](https://github.com/CMU-Perceptual-Computing-Lab/openpose) for details on OpenPose licensing. 
