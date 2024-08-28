# どんな情報がやり取りされているか知ろう！

## 概要

シミュレータの入出力についてまとめます

## I/O

### トピック

#### 入力

| トピック名         | 型                          | 説明 |
| ------------------ | --------------------------- | ---- |
| /cmd_vel           | [geometry_msgs/msg/Twist](http://docs.ros2.org/foxy/api/geometry_msgs/msg/Twist.html)     | ロボットの速度指令。線速度と角速度が含まれる。 |

#### 出力

| トピック名         | 型                          | 説明 |
| ------------------ | --------------------------- | ---- |
| /imu/data_raw      | [sensor_msgs/msg/Imu](http://docs.ros2.org/foxy/api/sensor_msgs/msg/Imu.html)         | IMUセンサーの生データ（加速度、角速度、方向）。 |
| /livox/lidar       | [sensor_msgs/msg/PointCloud2](http://docs.ros2.org/foxy/api/sensor_msgs/msg/PointCloud2.html) | LiDARからの3D点群データ。 |
| /odom              | [nav_msgs/msg/Odometry](http://docs.ros2.org/foxy/api/nav_msgs/msg/Odometry.html)       | ロボットの位置と速度情報。 |
| /robot_description | [std_msgs/msg/String](http://docs.ros2.org/foxy/api/std_msgs/msg/String.html)         | ロボットのモデル情報（URDF/SRDF）。 |
| /tf                | [tf2_msgs/msg/TFMessage](https://docs.ros2.org/foxy/api/tf2_msgs/msg/TFMessage.html)      | 動的な座標フレーム間の変換情報。 |
| /tf_static         | [tf2_msgs/msg/TFMessage](https://docs.ros2.org/foxy/api/tf2_msgs/msg/TFMessage.html)      | 静的な座標フレーム間の変換情報。 |


### サービス

#### 入力

| サービス名         | 型                          | 説明 |
| ------------------ | --------------------------- | ---- |
| /motor_power           | [std_srvs/srv/SetBool](https://docs.ros2.org/foxy/api/std_srvs/srv/SetBool.html)     | モータをON/OFFにする。 |