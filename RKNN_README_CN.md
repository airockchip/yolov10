# 导出 RKNPU2 适配模型说明

## Source

​本仓库基于 https://github.com/THU-MIG/yolov10 仓库的 62aaafb3a0bcc17224b797ae4e9af65d7f29773f commit 进行修改,验证.



## 模型差异

在不影响输出结果, 不需要重新训练模型的条件下, 有以下改动:

- 模型输出中置信度分支增加sigmoid算子(修改 `ultralytics/nn/modules/head.py`)

- 因后处理算子对推理性能和量化精度不友好，修改输出结构, 移除后处理结构(修改`ultralytics/nn/modules/head.py`)

- 为提升推理性能，移动 DFL 结构到模型外部的后处理阶段(修改`ultralytics/nn/modules/head.py`)


## 导出onnx模型

在满足`yolov10`原仓库中导出模型的安装环境后，执行以下语句导出模型

``` sh
yolo export model=model/yolov10{n/s/m/b/l/x} format=rknn opset=13 simplify

# model 为原始模型文件
# format 为模型导出格式
# 执行完毕后，会生成 ONNX 模型. 假如原始模型为 yolov10n.pt，则生成 yolo10n.onnx 模型。
```

## 转RKNN模型、Python demo、C demo

请参考 https://github.com/airockchip/rknn_model_zoo

