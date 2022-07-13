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
helm install athenaserving .  

## 等待AthenaServing服务组件全部启动成功后
helm install mmocr_ase .
```


## 配置Demo.py

```
image = open("demo_text_det.jpg","rb")     #待检测的图片
img = base64.b64encode(image.read())



url = "http://172.16.59.17:30889/mmocr"      # 30889要与mmocr服务暴露的端口相同
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

```