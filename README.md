# wit_ros_ws

# 安裝說明
## 1. 安裝 ROS IMU 依賴
如果你使用的是 Ubuntu 20.04，ROS Noetic，python3 :

```
$ sudo apt-get install ros-noetic-imu-tools ros-noetic-rviz-imu-plugin
$ pip3 install pyserial
```

## 2. 建立工作區
```
$ mkdir -p ~/wit_ros_ws/src
$ cd ~/wit_ros_ws/
$ catkin_make
```

## 3. 原始碼安裝 wit_ros
```
$ cd ~/wit_ros_ws/src
$ git clone https://github.com/Yuntechec404/wit_ros.git
$ catkin_make

# 設定執行檔案權限
$ cd ~/wit_ros_ws/src/wit_ros/scripts
$ sudo chmod 777 *.py

# 設定環境變數
$ echo "source ~/wit_ros_ws/devel/setup.sh" >> ~/.bashrc
$ source ~/.bashrc
```

# 使用範例
## 1. 查看 USB 埠號  
>  
先不要接上 IMU ，在終端機 (Terminal) 輸入 `ls  /dev/ttyUSB*` 檢測是否有其他設備，避免輸入錯誤埠號。  
將 IMU 接上電腦，再次於終端機輸入 `ls  /dev/ttyUSB*` ，多出來的 ttyUSB 設備就是 IMU 的埠號。

## 2. 修改参数配置  
需要修改的參數有：  
### Ⅰ. 設備類型  
> 
如果是 Modbus 通訊協議填 `modbus`，使用 wit 標準協議填 `normal`，如果是 MODBUS 高精度協議填 `hmodbus`，如果是 CAN 協議填 `can`，如果是CAN高精度協議填 `hcan`。

### Ⅱ. 埠號  
> 
腳本 (script) 默認使用 `/dev/ttyUSB0`，請根據你的電腦識別出來的埠號改寫。

### Ⅲ. 鮑率
> 
JY6x 系列默認為 115200，CAN 模組默認為 230400，其他默認為 9600。  
如果用戶通過[上位機](https://wit-motion.yuque.com/wumwnr/aqvq6y/vgr7u3)修改鮑率，則應對應修改鮑率。

## 3. 給埠號權限
```
$ sudo chmod 777 /dev/ttyUSB0
```

## 4. 啟動執行檔
```
$ roslaunch wit_ros_imu wit_imu.launch

# 經緯度數據只有 WIT 私有協議，即 normal 才有
$ rostopic echo /wit/imu
$ rostopic echo /wit/mag
$ rostopic echo /wit/location
```