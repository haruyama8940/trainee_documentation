# どんな情報がやり取りされているか知ろう！

## 概要

シミュレータの入出力についてまとめます

## I/O

### トピック

#### 入力

| トピック名         | 型                          | 説明 |
| ------------------ | --------------------------- | ---- |
| /cmd_vel           | geometry_msgs/msg/Twist     | ロボットの速度指令。線速度と角速度が含まれる。 |

#### 出力

| トピック名         | 型                          | 説明 |
| ------------------ | --------------------------- | ---- |
| /imu/data_raw      | sensor_msgs/msg/Imu         | IMUセンサーの生データ（加速度、角速度、方向）。 |
| /livox/lidar       | sensor_msgs/msg/PointCloud2 | LiDARからの3D点群データ。 |
| /odom              | nav_msgs/msg/Odometry       | ロボットの位置と速度情報。 |
| /robot_description | std_msgs/msg/String         | ロボットのモデル情報（URDF/SRDF）。 |
| /tf                | tf2_msgs/msg/TFMessage      | 動的な座標フレーム間の変換情報。 |
| /tf_static         | tf2_msgs/msg/TFMessage      | 静的な座標フレーム間の変換情報。 |


### サービス

#### 入力

| サービス名         | 型                          | 説明 |
| ------------------ | --------------------------- | ---- |
| /motor_power           | std_srvs/srv/SetBool     | モータをON/OFFにする。 |