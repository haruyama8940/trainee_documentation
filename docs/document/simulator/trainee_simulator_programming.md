# トピックからメッセージを受け取ってみよう！

## 概要
どうやって情報を受け取ってプログラミングをしていけばいいのか説明します（C++）

## IMUのデータを取得しよう

### コードを書く

* imu_subscriber.cpp

``` c++ linenums="1"
#include <rclcpp/rclcpp.hpp>
#include <sensor_msgs/msg/imu.hpp>

class ImuSubscriber : public rclcpp::Node
{
public:
  ImuSubscriber() : Node("imu_subscriber")
  {
    subscription_ = this->create_subscription<sensor_msgs::msg::Imu>(
      "imu/data_raw", 10, std::bind(&ImuSubscriber::topic_callback, this, std::placeholders::_1));
  }

private:
  void topic_callback(const sensor_msgs::msg::Imu::SharedPtr msg) const
  {
    RCLCPP_INFO(this->get_logger(), "Received IMU data:");
    RCLCPP_INFO(this->get_logger(), "Orientation -> x: %.2f, y: %.2f, z: %.2f, w: %.2f",
                msg->orientation.x, msg->orientation.y, msg->orientation.z, msg->orientation.w);
    RCLCPP_INFO(this->get_logger(), "Angular Velocity -> x: %.2f, y: %.2f, z: %.2f",
                msg->angular_velocity.x, msg->angular_velocity.y, msg->angular_velocity.z);
    RCLCPP_INFO(this->get_logger(), "Linear Acceleration -> x: %.2f, y: %.2f, z: %.2f",
                msg->linear_acceleration.x, msg->linear_acceleration.y, msg->linear_acceleration.z);
  }

  rclcpp::Subscription<sensor_msgs::msg::Imu>::SharedPtr subscription_;
};

int main(int argc, char *argv[])
{
  rclcpp::init(argc, argv);
  rclcpp::spin(std::make_shared<ImuSubscriber>());
  rclcpp::shutdown();
  return 0;
}
```

### ビルド & 実行のためにパッケージづくり

CMakeLists.txtとpackage.xmlを用意しましょう

* CMakeLists.txt

``` cmake
cmake_minimum_required(VERSION 3.8)
project(imu_subscriber)

find_package(ament_cmake_auto REQUIRED)

ament_auto_find_build_dependencies()

ament_auto_add_executable(imu_subscriber
  src/imu_subscriber.cpp
)

ament_auto_package(
  INSTALL_TO_SHARE
)
```

* package.xml

``` xml
<package format="3">
  <name>imu_subscriber</name>
  <version>0.0.0</version>
  <description>IMU Subscriber Node</description>

  <maintainer email="user@example.com">Your Name</maintainer>
  <license>Apache-2.0</license>

  <buildtool_depend>ament_cmake_auto</buildtool_depend>
  <depend>rclcpp</depend>
  <depend>sensor_msgs</depend>

  <export>
    <build_type>ament_cmake</build_type>
  </export>
</package>
```

### ビルド & 実行

* ビルド
``` sh
colcon build --symlink-install
source install/setup.bash 
```

* 実行
``` sh
ros2 launch raspicat_map2gazebo raspicat_tsukuba2023_world.launch 
ros2 run imu_subscriber imu_subscriber
```