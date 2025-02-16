# Simple_ROMP

Simplified implementation of ROMP: Monocular, One-stage, Regression of Multiple 3D People, ICCV21

Please refer to https://github.com/Arthur151/ROMP for more details

## Installation

```
pip install --upgrade setuptools numpy cython
```

```
pip install --upgrade simple_romp
```
or download the package and install it from source:
```
python setup.py install
```

For Mac users, we strongly recommand to upgrade your pytorch to the latest version to support more basic operations used in BEV. To achieve this, please run
```
pip install --upgrade torch torchvision
```

## Usage

Webcam demo:
```
romp --mode=webcam --show 
bev --mode=webcam --show
```
For faster inference with romp on CPU, you may run `romp --mode=webcam --show --onnx` instead.  
For Mac Users, please use the original terminal instead of other terminal app (e.g. iTerm2) to avoid the bug `zsh: abort`.

<p float="center">
  <img src="../../assets/demo/animation/image_demo2-min.gif" width="32%" />
  <img src="../../assets/demo/animation/Solvay_conference_1927_all_people.png" width="32%" />
  <img src="../../assets/demo/animation/conference_mesh_rotating.gif" width="32%" /></div>
</p>
</p>

In this [folder](https://github.com/Arthur151/ROMP/tree/assets/demo/BEV_demo_images), we prepare some demo images for testing.

Processing a single image:
```
romp --mode=image --calc_smpl --render_mesh --input=/path/to/image.jpg --save_path=/path/to/results.jpg
bev -i /path/to/image.jpg -o /path/to/results.jpg
```

Processing a folder of images:
```
romp --mode=video --calc_smpl --render_mesh  --input=/path/to/image/folder/ --save_path=/path/to/output/folder/
bev -m video -i /path/to/image/folder/ -o /path/to/output/folder/
```
<p float="center">
  <img src="../../assets/demo/animation/c1_results_compressed.gif" width="32%" />
  <img src="../../assets/demo/animation/c4_results_compressed.gif" width="32%" />
  <img src="../../assets/demo/animation/c0_results_compressed.gif" width="32%" />
</p>


Processing a video:
```
romp --mode=video --calc_smpl --render_mesh  --input=/path/to/video.mp4 --save_path=/path/to/output/folder/results.mp4 --save_video
bev -m video -i /path/to/video.mp4 -o /path/to/output/folder/results.mp4 --save_video
```

Common optional functions:
```
# show the results during processing image / video, add:
--show

# items you want to visualized, including mesh,pj2d,j3d,mesh_bird_view,mesh_side_view,center_conf,rotate_mesh. Please add if you want to see more:
--show_items=mesh,mesh_bird_view
```

ROMP only optional functions:
```
# to smooth the results in webcam / video processing, add: (the smaller the smooth_coeff, the smoother) 
--temporal_optimize --smooth_coeff=3.

# to use the onnx version of ROMP for faster inference, please add:
--onnx

# to show the largest person only (remove the small subjects in background), add:
--show_largest 
```
<p float="center">
<img src="../../assets/demo/animation/video_demo_nofp.gif" width="32%" />
  <img src="../../assets/demo/animation/video_demo_fp.gif" width="40%" />
</p>
More options, see `romp -h`

Note that if you are using CPU for ROMP inference, we highly recommand to add `--onnx` for much faster speed.

### Tools
To convert the trained ROMP model '.pkl' (like ROMP.pkl) to simple-romp '.pth' model, please run
```
cd /path/to/ROMP/simple_romp/
python tools/convert_checkpoints.py ROMP.pkl ROMP.pth
```

## Copyright

Codes released under MIT license. All rights reserved by Yu Sun.
