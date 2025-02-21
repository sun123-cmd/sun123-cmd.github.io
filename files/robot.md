# 车臂机器人快速上手

## 1. 机器人硬件配置

* 底盘：dalu
* 机械臂：UR3
* 相机：Intel D435*2
* 雷达：思岚科技A2

## 2. 机器人连接

### 2.1 无线连接（推荐）

* 首先，打开机器人底盘和机械臂上的电源

* 然后，服务器连接wifi：`USR-G810-A0B9`，密码：`www.usr.cn`

* 接下来，固定服务器Wi-Fi 的IP为`192.168.6.36`，机器人IP保持`192.168.6.102`不变，能ping通就连好了

* 最后需要设置ROS网络，服务器上已经配置好：

  ```
  export  ROS_IP=192.168.6.36
  export  HOSTNAME=192.168.6.36
  export  ROS_MASTER_URI=http://192.168.6.102:11311/
  ```

## 2.2 有线连接

* 把机器人上蓝色的网线插到电脑上，按照无线方式固定IP，能ping通即可，同理进行ROS组网

### 3. 机器人使用

网络配置好后，ssh到机器人上，密码：`a`：

```
ssh maiya@192.168.6.102
source ~/.bashrc
```

这样就激活了机器人上的ROS环境

### 3.1 扫图

首先需要在本地机器打开RVIZ：

```
rviz
```

然后打开RVIZ最近打开的项目模版，可以实时查看扫图情况，同时在机器人上：

```
roslaunch dalu robot.launch
roslaunch dalu cartographer_mapping.launch use_sim_time:=false
```

这样就启动好了扫描配置，然后打开键盘控制：

```
roslaunch coffe_teleops keyboard_teleop.launch
```

通过控制键盘来控制机器人导航，就可以扫图，扫好后保存结果：

```
rosservice call /write_state "{filename: '/home/maiya/maps/demo0425.pbstream'}" #根据日期改名字
```

### 3.2 导航

图扫好后，配置机器人上的`location.launch`脚本，把地图修改为刚刚建立的最新的

然后启动：

```
roslaunch dalu localization.launch
```

就可以在rviz里根据箭头控制位置导航，或者在terminal发送goal导航

也可以采取下列方式手动导航，如果开启`keyboard_teleop`，给定goal的导航会被中断，这个办法也可以用于**自动导航时的急停**：

```
roslaunch coffe_teleops keyboard_teleop.launch
```

### 3.3 抓取

需要启动控制机械臂和爪子的脚本：

```
roslaunch visual_servo GripperControl.launch
roslaunch visual_servo uGraspControl.launch 
```

启动后，可以在服务器上`/home/disk1/dalu/task_planner.py`中修改命令执行对应目标的语义抓取：

```
cd /home/hs/disk1/dalu
conda activate grasp-env
python main.py
```

自定义机械臂行为，可以在机器人上`visual_servo`包中参考`uGraspControl`的方式修改,修改后需要重新编译包：

```
catkin_make -DCATKIN_WHITELIST_PACKAGES="visual_servo"
```

### 3.4 最好上手的操作

导航、抓、放，都可以直接修改`/home/disk1/dalu/task_planner.py`中的task来实现，参考脚本中的配置方式即可，修改task后直接运行`main.py`即可

## 4. 一些说明

* 机器人上的代码古早，依赖复杂，不要轻易更新内部的环境（如gcc、python版本等）

* 机器人硬件不稳定，使用时尽量避免磕碰，撞坏了很麻烦
* 机器人电池不安全，充电不宜太久，人走断电，也不要边充电边使用机器人