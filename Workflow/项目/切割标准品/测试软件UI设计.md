
| 文件导入 | 设备调试           | 流程：通用         | 流程：粗定位     | 流程：精定位     | 切割参数 | 变量查询&改写 |
| -------- | ------------------ | ------------------ | ---------------- | ---------------- | -------- | ------------- |
| 导入dwg  | Ping机器人         | 机器人=>初始化变量 | 机器人=>拍照位置 | 计算扫描点       |          | 变量名称      |
| 导入Json | Ping相机           | 计算切割路径       | 相机=>拍摄新数据 | 机器人=>扫描路径 |          | 变量类型      |
| 选择工件 | Ping线激光         | 机器人=>切割路径   | 相机=>新工件     | 模型重构         |          | 查询          |
|          | 连接机器人         | 机器人=>工件轮廓   |                  |                  |          | 重写          |
|          | 连接相机           |                    |                  |                  |          |               |
|          | 连接线激光         |                    |                  |                  |          |               |
|          | 获取机器人连接状态 |                    |                  |                  |          |               |
|          | 获取相机连接状态   |                    |                  |                  |          |               |
|          | 获取线激光连接状态 |                    |                  |                  |          |               |
|          |                    |                    |                  |                  |          |               |

