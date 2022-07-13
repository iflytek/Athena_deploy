# AthenaServing&Mmocr
[![Build Status](https://travis-ci.com/xfyun/AthenaServing.svg?branch=master)](https://travis-ci.com/xfyun/AthenaServing)
[![Language](https://img.shields.io/badge/Language-Go-blue.svg)](https://golang.org/)
[![License](https://img.shields.io/badge/License-Apache%202.0-blue.svg)](https://github.com/xfyun/AthenaServing/blob/master/LICENSE)

>通过 AthenaServing & Mmocr 共同构建可用的物体检测Ai能力服务。整套流程体现了AthenaServing如何高效部署Ai能力模型，方便用户完成训练模型的快速部署与上线。

## 前置条件
 - 部署 k8s集群
 - 安装 helm

## Install 
```
cd chart
helm install athena . 

## 等待AthenaServing服务组件全部启动成功后
helm  install mmocr .
```


## 配置Demo.py

```
image = open("demo_text_det.jpg","rb")     #待检测的图片
img = base64.b64encode(image.read())


url = "http://172.16.59.17:30889/mmocr"    # url 可以是 hostIP:nodePort 也可以是 svcIP:svcPort   
url = "http://172.16.59.17:30889/v1/private/mmocr"
method = "POST"
headers = {"Content-Type":"application/json"}
data = {
    "header": {
        "app_id": "123456",
        "uid": "39769795890",
        "did": "SR082321940000200",
        "imei": "8664020318693660",
        "imsi": "4600264952729100",
        "mac": "6c:92:bf:65:c6:14",
        "net_type": "wifi",
        "net_isp": "CMCC",
        "status": 3,
        "request_id": None
    },
    "parameter": {
        "mmocr": {
            "category": "ai_category",
            "application_mode": "common_gpu",
            "gpu_id": "first",
            "gpu_type": "T4G16",
            "boxes": {
                "encoding": "utf8",
                "compress": "raw",
                "format": "json"
            }
        }
    },
    "payload": {
        "data": {
            "encoding": "jpg",
            "image": img.decode("utf-8"),
            "status": 3
        }
    }
}

```


## 测试Demo.py
```
python demo.py
```

## 结果展示

```
##################################
MMocr Result: box located at [190, 37, 253, 31, 254, 46, 191, 52], box score is 0.9566415548324585.  Detected text is nboroughofs, text  score is 1.0...
MMocr Result: box located at [253, 47, 257, 36, 287, 47, 282, 58], box score is 0.9649642705917358.  Detected text is fsouthw, text  score is 1.0...
MMocr Result: box located at [157, 59, 188, 41, 194, 52, 163, 70], box score is 0.9521175622940063.  Detected text is londond, text  score is 0.9897959183673469...
MMocr Result: box located at [280, 58, 286, 50, 306, 67, 300, 74], box score is 0.9397557377815247.  Detected text is thwark, text  score is 1.0...
...
```