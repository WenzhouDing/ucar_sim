#  重要更新:

models已更新至由主办方提供的图片制作的图片识别板

> 若使用过此包旧版本的仿真，需要重新执行使用方法下的步骤3

world文件夹下的arena-1, arena-2, arena-3 分别为三套仿真比赛

> 图像识别板的位置参考了赛前会议抽取的三套识别板摆放位置，图像内容组合非参考比赛题库中的组合
> (详见：抽取结果.pdf, img-floder)

![image](https://github.com/wenchowD/ucar_sim/blob/main/img-folder/32images.png)



#  效果图:

仿真场地中使用同终点地块图样的地块来标记随机图像板以及固定图像板的位置

> 图像板详细坐标区域的信息需参见：抽取结果.pdf, img-folder/map.png

![image](https://github.com/wenchowD/ucar_sim/blob/main/img-folder/arena.png)



#  使用方法：

1. 将ucar_sim包复制到工作空间src目录下

     

2. 先catkin_make编译，再 source ~/.bashrc 或 devel/setup.bash

   > 为了防止启动时编码报错，更改 python2 的默认编码
   > 解决方案：
   > 打开终端输入如下指令 ( 使用 anaconda 的同学要定位到自己的虚拟环境 )：

   >   ```
   >   sudo gedit /usr/lib/python2.7/site.py
   >   ```

   > 找到 setencoding() 函数
   > 修改第 一 个 encoding="utf-8"
   > 重启电脑

   

3. 把ucar_sim包中的models文件夹内的东西全部复制到.gazebo/models下

     > (.gazebo为隐藏文件，如果没有models请自行创建此文件夹)
     >  前提：没有打开过gazebo的同学，请在终端中输入gazebo运行一次

     

4. 运行比赛的仿真

     ```
     roslaunch ucar_sim simulation.launch
     ```

     > 其他情况：
     > 现象： 在终端出现
     > Gazebo [Err] [REST.cc:205] Error in REST request
     > 解决方法：
     > 打开终端输入：

     > ```
     > sudo gedit ~/.ignition/fuel/config.yaml
     > ```

     > 用 url: https://api.ignitionrobotics.org 替换 url : https://api.ignitionfuel.org




#  Package说明：

- 包内的models文件夹在完成了上述的操作后便不再需要
- meshes文件夹包含模型的文件无需修改



1. world文件夹存储仿真用的世界

   下有arena-empty.world arena-1.world，分别为空场地和模拟比赛的场地

   

2. urdf文件夹存储机器人描述文件

   xacro文件包含机器人的长，宽，高，颜色，传感器等信息，我已根据比赛使用的机器人做了相应的修改

   

3. launch文件夹存储启动文件

   修改可选择所启动的世界，和机器人出生位置（当前为启动arena-1.world，出生在比赛起点）

   

4. 修改视觉识别任务的目标图片

   进入.gazebo/models目录，找到需要替换的类别对应的文件夹（e.g. 05-person-1）并进入该文件夹

   替换 materials/textures目录下的 XXX.png（e.g. 05-person-1.png）

   注意图片格式为png且名称保持前后一致



#  编辑自己的场地：

1. 终端输入以下命令来导入一个现成的世界：

   gazebo /XXX_ws/src/ucar_sim/world/XXX.world (替换成自己的存储.world文件的地址)

   

2. gazebo图形界面左上角点击Insert，再点击想要添加的模型名称可向世界添加模型

   

3. gazebo图形界面上方可调整模型位置以及姿态

   *.更多操作请见参考



# 参考：

画墙：https://classic.gazebosim.org/tutorials?cat=build_world&tut=building_editor

贴图：https://www.guyuehome.com/37739

URDF：略

