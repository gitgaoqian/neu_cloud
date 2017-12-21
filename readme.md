云端运行程序：cloud_server.py
本地运行程序：bridge.py client.py　
其中bridge.py是桥梁通信节点，负责和云端的通信．
client.py是服务请求节点，和桥梁通信节点以ros　srv形式通信，其需要接受两个外部参数，分别表示服务名称和对服务采取的动作（start or stop）
以申请＂vision＂为例，阐述具体服务的申请流程：
１为减少操作，本地创建launch文件，服务名称和服务动作也写入参数服务器中
<launch>
  <node pkg="neuro_cloud" type="bridge.py" name="bridge" output="screen">
  </node>
  <node pkg="neuro_cloud" type="client.py" name="client" output="screen">
    <param name="service" value="stereo_proc" />
    <param name="action" value="start"/>
  </node>
</launch>
２　首先运行cloud_server.py,然后运行本地launchwen文件，云端会自动获取本地服务申请端的IP，并将云端的ROS_MASTER_URI配置本地的rosmaster,同时启动所有与"vision"服务相关的节点，那么云端就可以处理本地传输的图像．
