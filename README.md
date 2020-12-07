# Human pose estimation algorithms easy to use

## Requirements

* Windows/MacOS/Linux
* [Docker client](https://www.docker.com/products/docker-desktop)
* Optional: [NVIDIA docker](https://github.com/NVIDIA/nvidia-docker) for GPU support (10x faster processing)

## OpenPose

OpenPose returns 2d keypoints for each frame in the video. See [OpenPose repository](https://github.com/CMU-Perceptual-Computing-Lab/openpose) for details.

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

GPU processing is much faster (around real time) but it requires a GPU and NVIDIA docker. For GPU processing run:
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

docker run --gpus all --rm -v $(pwd)/input:/data/input -v $(pwd)/output:/data/output -v $(pwd)/models:/data/models -it vid2osim

## VideoPose3D

VideoPose3D returns 3d keypoints for each frame in the video. See [VideoPose3D repository](https://github.com/facebookresearch/VideoPose3D) for details.

**GPU and NVIDIA docker are required to run this software**

Create `input`, `output`, and `models` directories. Put your `mp4` video in the `input` directory.

Run
```
docker run --gpus all --rm\
  -v $(pwd)/input:/data/input\
  -v $(pwd)/output:/data/output\
  -v $(pwd)/models:/data/models\
  -it stanfordnmbl/videopose3d
```

Results will be saved in `output`.

In the first run, deep learning models will be downloaded to `models` directory which can take some time. These models will be saved for all subsequent runs which will make it much faster. 

## License

In this repository we only provide instructions on how to run software. Corresponding licenses apply.

* OpenPose: See [OpenPose repository](https://github.com/CMU-Perceptual-Computing-Lab/openpose)
* VideoPose3D: See [VideoPose3D repository](https://github.com/facebookresearch/VideoPose3D)
