# RKNN optimization for exporting model

## Source
Base on https://github.com/THU-MIG/yolov10 with commit id as 62aaafb3a0bcc17224b797ae4e9af65d7f29773f


## What different
With inference result values unchanged, the following optimizations were applied:

- Added a sigmoid operator to the confidence branch in the model output (Modify `ultralytics/nn/modules/head.py`).

- Removed the post-processing structure from the output to improve inference performance and quantization precision, as the original post-processing operators were not friendly to these aspects (Modify `ultralytics/nn/modules/head.py`).

- To enhance inference performance, the DFL (Distribution Focal Loss) structure has been moved to the post-processing stage outside of the model (Modify `ultralytics/nn/modules/head.py`).


## Export ONNX model

After meeting the installation environment requirements in the original `yolov10` repository for exporting the model, execute the following command to export the model:


``` sh
yolo export model=model/yolov10{n/s/m/b/l/x} format=rknn opset=13 simplify

# model refers to the original model file.
# format refers to the model weight file.
# After execution, an ONNX model will be generated. If the original model is yolov10n.pt, the generated ONNX model will be yolo10n.onnx.
```

## Convert to RKNN model, Python demo, C demo

Please refer to https://github.com/airockchip/rknn_model_zoo.
