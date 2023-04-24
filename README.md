# 点击选择文字验证码识别
文字点选、选字、选择文字验证码识别  
- 特点
``` 
识别速度约在100~300ms之间  
96%的准确率  
小样本训练（此模型训练采用了300张验证码）  
windows下python3.6、python3.8、python3.10测试使用通过  
低消耗，代码经编译后在低配置机器上也可运行（1核2G服务器无压力运行）  
```
## 效果演示
![Image text](./docs/res.gif)  

## 免责声明
**本项目旨在研究深度学习在验证码攻防上的应用。仅供学习交流使用，请勿用于非法用途，不得在任何商业使用，本人不承担任何法律责任。**

# 请作者喝可乐**o(*￣︶￣*)o**  

| Wechat Pay | Ali Pay |
| --- | --- |
| <img src="./docs/wechat.jpg" height="300" /> | <img src="./docs/Ali.png" height="300" /> |

## 如何使用
``` bash
1、准备运行环境：
pip install -r requirements.txt
2、普通使用：
python dome.py
3、服务启动方式，启动后访问http://127.0.0.1:8000/docs#/查看接口文档
python service.py
4、bilbil演示”
python bilbil.py
```  
结果如下：  
```json
[
  [123, 174, 190, 243],
  [222, 188, 295, 265],
  [84, 72, 158, 138],
  [32, 197, 107, 279]
]
```
| 原始 | 检测 | 识别 |
| --- | --- |--- |
| <img src="./docs/res.jpg" width="300" height="300"> | <img src="./docs/res1.jpg" width="300" height="300"> | <img src="./docs/res2.jpg" width="300" height="300">|

## 更新说明
#### 2023.04.23更新: 更改检测识别模型，修改返回结构  
## 后续更新计划
增加支持其他类型的点选验证码  
旋转验证码感觉还蛮有意思的 有空可以搞一搞  

#实现流程
- 问题拆解  
**对于点选式验证码的问题，我们可以将其拆解为两个小问题：**  
  1、**确定需要点击的字的数量和位置：** 对于点选式验证码，准确识别和定位需要点击的字的数量和位置是解决问题的关键。其中，一种常见的目标检测算法是 YOLO，通过标注数据集和训练模型，可以实现对需要点击的字进行准确识别和定位。本项目采用的是 yolov5 模型，该模型在目标检测方面表现出色，具有高速和较高的准确性。  
  2、**对点击的字进行排序：** 在确定出需要点击的字的位置后，需要按照一定的规则对这些字进行排序。采用传统的方案是通过识别图片中的文字，然后按照文字位置进行排序，但这种方法训练困难。因此，本项目采用了图片匹配模型，使用 Siamese 孪生网络对需要点击的字与预先准备好的字库中的字进行匹配，找到最佳匹配的字，并按照一定的规则进行排序。Siamese 孪生网络在图像匹配方面表现优异，能够有效地提高排序的准确性和稳定性。
- 训练模型  
  ***训练代码在下方参考文档中***  
    **yolov5训练过程**  
        pass
    **Siamese训练过程**  
        pass
- 推理部署

推理部署过程是将 YOLO 和 Siamese 模型都转换为 ONNX 模型，以便在 CPU 上使用模型，并提高部署难度和运行速度。通过模型转换，可以将模型从原有的深度学习框架中的特定格式转换成 ONNX 格式，使得模型可以在多个平台上使用，并且可以在不同的编程语言之间轻松交互。  
**onnx介绍：**
```
ONNX，即开放神经网络交换格式（Open Neural Network Exchange），是一个可以让不同深度学习框架之间互相转换和使用模型的开放标准。它由 Facebook 和 Microsoft 共同开发，旨在为深度学习模型的部署和迁移提供更加方便和灵活的解决方案。ONNX 支持包括 PyTorch、TensorFlow、CNTK 和 MXNet 等在内的多个深度学习框架，可以将这些框架训练出的模型转换成 ONNX 格式，从而可以被其他框架或应用所使用。

ONNX 的主要优点包括：

互操作性好：ONNX 支持多个深度学习框架之间的模型转换，使得它们可以互相使用和部署，从而减少了开发和部署的难度和成本；

高效性能：ONNX 可以在多种硬件和软件平台上运行，并提供了 C++和 Python 接口，可以大幅提高模型执行的效率和速度；

易于扩展：ONNX 的架构简单清晰，可以轻松地添加新的层次和类型，方便应对不断升级变化的深度学习技术和需求。

总之，ONNX 是一个方便快捷的深度学习模型转换和交换标准，可以帮助开发者更加轻松地将深度学习模型进行部署和迁移。
```
在将模型转换为 ONNX 格式后，对代码进行编译也是必不可少的一步。通过编译，可以将 Python 代码转换成机器语言代码，进一步提高模型的运行效率和速度。同时，也可以减少代码的存储空间，使得模型能够更快地在 CPU 上加载和运行。
###  参考文档
https://github.com/ultralytics/yolov5  
https://github.com/bubbliiiing/Siamese-pytorch

## 有什么问题或需求欢迎各位在lssues中提问或联系邮件**yj970814@163.com**
### 点个**star**再走呗！ 