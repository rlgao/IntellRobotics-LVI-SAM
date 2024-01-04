# LVI_SAM

## To run

- In one terminal: 

```shell
cd ~/lvisam_ws
source devel/setup.bash
roslaunch lvi_sam Husky.launch
```
- In the other terminal: 

```shell
cd ~/rosbags/lvi-sam
rosbag play husky.bag
```

- Useful TF commands:

```shell
rosrun rqt_tf_tree rqt_tf_tree
rosrun tf view_frames
```



## To evaluate

```shell
# pcd转txt，位于~/lvi-sam/src/LVI-SAM-Easyused/pcd2tum.py
# pip install pyntcloud
python pcd2tum.py
```
- 安装evo评估工具
```shell
# https://github.com/MichaelGrupp/evo
pip install evo --upgrade --no-binary evo
```
- 拷贝真值轨迹, gt.txt
```shell
~/lvi-sam/results/gt.txt
```
- 计算误差
```shell
# -r full (旋转+平移) trans_part (平移m) angle_deg (旋转deg)
evo_ape tum gt.txt lvisam.txt -r full -va --plot --plot_mode xy --save_plot ./lvisamplot
# 多轨迹绘制
# evo_traj tum lvisam.txt fastlio2.txt kissicp.txt --ref=gt.txt -va -p --plot_mode=xy --save_plot ./trajall
```

## Parameters

- `Husky_camera.yaml` and `Husky_lidar.yaml`
- Camera intrinsics
- Camera-IMU, LiDAR-IMU extrinsics

## Acknowledgement

- Original [LVI-SAM](https://github.com/TixiaoShan/LVI-SAM)
- Modified [LVI-SAM-Easyused](https://github.com/NeSC-IV/LVI-SAM-Easyused)

