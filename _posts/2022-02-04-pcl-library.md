---
layout: post
toc: true
title: "PCL 101"
categories: [PCL, '101']
---
## References

## What is PCL?
**Point Cloud Library**는 LiDAR나 RGB-D 카메라를 통해 취득한 pointcloud를 후처리하는데 사용되는 알고리즘을 구현해둔 라이브러리다. 

## Part 0. Declaration
`pcl::PointCloud<T>`의 T 자리에 다양한 type을 담을 수 있다. <br> 
LiDAR 사용 시에는 `pcl::PointXYZ`, `pcl::PointXYZI`를 사용하는 편이다. RGB-D 데이터에는 `pcl::PointXYZRGB`를 사용한다.
Pointcloud는 `std::vector`의 자료구조로 구현되어 있으며, 따라서 `std::vector`가 가지고 있는 여러 문법을 지원한다.

```c++
pcl::PointCloud<pcl::PointXYZ> cloud;

pcl::PointXYZ point_xyz;
point_xyz.x = 1;
point_xyz.y = 2;
point_xyz.z = 3;

pcl::PointXYZ point_xyz = {1, 2, 3}; // Initialization
```

## Part 1. Useful Functions
기본적인 concept을 PointCloud 객체를 Point들을 담고 있는 std::vector로, 각 원소는 Point들로 생각하면 이해하기 쉬움.

`resize`: cloud의 size를 재조정
`front`
`end`
`begin`
`back`
`at`
`empty`
`clear`
`+=`: shallow copy of point cloud

모든 함수를 활용한 예제는 아래에 있다.
```c++
pcl::PointCloud<PointXYZ> cloud;
cloud.resize(5);

cloud.points[0].x = 1; cloud.points[0].y = 2; cloud.points[0].z = 3;
pcl::PointXYZ point;
point.x = 4; point.y = 5; point.z=6;
cloud.push_back(point);

cout << cloud.begin()->x << endl;
cout << cloud.end()->x << endl; // next to last (ERROR!)
cout << (cloud.end()-1)->x << endl;
cout << cloud.front().x << endl;
cout << cloud.at(1).x << endl;
```

## Part 2. 형변환 
ROS에서 master를 통해 통신할 때 `sensor_msgs::PointCloud2` 메시지를 사용하는데, 그 data를 후처리할 때는 PCL의 pointcloud를 사용해야 하기 때문에 우리는 publish할 때 형변환 과정을 반드시 거쳐야 한다!
(`sensor_msgs::PointCloud2`를 쓰는 이유는 range data를 publish하는 것이 raw하게 publish하는 것보다 더 효율적이기 때문이라고 추정)

**sensor_msgs::Pointcloud2 -> pcl::PointCloud**
```c++
pcl::PointCloud<pcl::PointXYZ> cloudmsg2cloud(sensor_msgs::PointCloud2 cloud){
    pcl::PointCloud<pcl::PointXYZ> cloud_dst;
    pcl::fromROSMsg(cloudmsg, cloud_dst);
    return cloud_dst;d
}
```

**pcl::PointCloud->sensor_msgs::PointCloud2**
```c++
sensor_msgs::PointCloud2 cloud2cloudmsg(pcl::PointCloud<pcl::PointXYZ> cloud_src){
    sensor_msgs::PointCloud2 cloudmsg;
    pcl::toROSMsg(cloudsrc, cloudmsg);
    cloudmsg.header.frame_id = "map";
    return cloudmsg;
}
```

## Part 3. Transformation
Pointcloud이 가장 먼저 인식될 때에는 보통 LiDAR나 radar 등 특정 frame을 기준으로 그 좌표 값들이 형성된다. 따라서, point cloud를 적절하게 transform 해주는 작업이 필요하다.

```c++
pcl::PointCloud<pcl::PointXYZ> cloud_src;
pcl::PointCloud<pcl::PointXYZ>::Ptr ptr_transformed(new pcl::PointCloud<pcl::PointXYZ>);

Eigen::Matrix4f trans;
trans << 1, 0, 0, 0.165,
        0, 1, 0, 0.000,
        0, 0, 1, 0.320,
        0, 0, 0, 1;
pcl::transformPointCloud(cloud_src, *ptr_transformed, trans);
pc_transformed = *ptr_transformed;
```