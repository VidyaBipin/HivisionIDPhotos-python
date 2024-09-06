<div align="center">

<img alt="hivision_logo" src="assets/hivision_logo.png" width=120 height=120>
<h1>HivisionIDPhoto</h1>

[English](README_EN.md) / 中文 / [日本語](README_JP.md) / [한국어](README_KO.md)

[![GitHub](https://img.shields.io/static/v1?label=GitHub&message=GitHub&color=black)](https://github.com/xiaolin199912/HivisionIDPhotos)
[![GitHub stars](https://img.shields.io/github/stars/zeyi-lin/hivisionidphotos)](https://github.com/zeyi-lin/hivisionidphotos/stargazers)
[![SwanHub Demo](https://swanhub.co/git/repo/SwanHub%2FAuto-README/file/preview?ref=main&path=swanhub.svg)](https://swanhub.co/ZeYiLin/HivisionIDPhotos/demo)
[![Spaces](https://img.shields.io/badge/🤗-Open%20in%20Spaces-blue)](https://huggingface.co/spaces/TheEeeeLin/HivisionIDPhotos)
<a href="https://docs.qq.com/doc/DUkpBdk90eWZFS2JW" target="_blank">
<img alt="Static Badge" src="https://img.shields.io/badge/WeChat-微信-4cb55e"></a>

<!-- <a href="https://trendshift.io/repositories/11622" target="_blank"><img src="https://trendshift.io/api/badge/repositories/11622" alt="Zeyi-Lin%2FHivisionIDPhotos | Trendshift" style="width: 250px; height: 55px;" width="250" height="55"/></a>

<a href="https://hellogithub.com/repository/8ea1457289fb4062ba661e5299e733d6" target="_blank"><img src="https://abroad.hellogithub.com/v1/widgets/recommend.svg?rid=8ea1457289fb4062ba661e5299e733d6&claim_uid=Oh5UaGjfrblg0yZ" alt="Featured｜HelloGitHub" style="width: 250px; height: 54px;" width="250" height="54" /></a> -->

[![Spaces](https://trendshift.io/api/badge/repositories/11622)](https://trendshift.io/repositories/11622)

[![Spaces](https://abroad.hellogithub.com/v1/widgets/recommend.svg?rid=8ea1457289fb4062ba661e5299e733d6&claim_uid=Oh5UaGjfrblg0yZ)](https://hellogithub.com/repository/8ea1457289fb4062ba661e5299e733d6)

<img src="assets/demoImage.png" width=900>

</div>

<br>

> **相关项目**：
>
> - [SwanLab](https://github.com/SwanHubX/SwanLab)：训练人像抠图模型全程用它来分析和监控，以及和实验室同学协作交流，大幅提升了训练效率。

<br>

# 🤩 项目更新

- 在线体验： [![SwanHub Demo](https://img.shields.io/static/v1?label=Demo&message=SwanHub%20Demo&color=blue)](https://swanhub.co/ZeYiLin/HivisionIDPhotos/demo)、[![Spaces](https://img.shields.io/badge/🤗-Open%20in%20Spaces-blue)](https://huggingface.co/spaces/TheEeeeLin/HivisionIDPhotos)

- 2024.9.6: 增加新的抠图模型 [modnet_photographic_portrait_matting.onnx](https://github.com/ZHKKKe/MODNet)
- 2024.9.5: 更新 [Restful API 文档](docs/api_CN.md)
- 2024.9.2: 更新**调整照片 KB 大小**，[DockerHub](https://hub.docker.com/r/linzeyi/hivision_idphotos/tags)
- 2023.12.1: 更新**API 部署（基于 fastapi）**
- 2023.6.20: 更新**预设尺寸菜单**
- 2023.6.19: 更新**排版照**

# Overview

> 🚀 谢谢你对我们的工作感兴趣。您可能还想查看我们在图像领域的其他成果，欢迎来信:zeyi.lin@swanhub.co.

HivisionIDPhoto 旨在开发一种实用的证件照智能制作算法。

它利用一套完善的模型工作流程，实现对多种用户拍照场景的识别、抠图与证件照生成。

**HivisionIDPhoto 可以做到：**

1. 轻量级抠图（仅需 **CPU** 即可快速推理）
2. 根据不同尺寸规格生成不同的标准证件照、六寸排版照
3. 美颜（waiting）
4. 智能换正装（waiting）

<div align="center">
<img src="assets/harry.png" width=900>
</div>

<!-- <div align="center">
<img src="assets/gradio-image.jpeg" width=900>
</div> -->

---

如果 HivisionIDPhoto 对你有帮助，请 star 这个 repo 或推荐给你的朋友，解决证件照应急制作问题！

<br>

# 🔧 环境安装与依赖

- Python >= 3.7（项目主要测试在 python 3.10）
- onnxruntime
- OpenCV
- Option: Linux, Windows, MacOS

**1. 克隆项目**

```bash
git clone https://github.com/Zeyi-Lin/HivisionIDPhotos.git
cd  HivisionIDPhotos
```

**2. （重要）安装依赖环境**

> 建议 conda 创建一个 python3.10 虚拟环境后，执行以下命令

```bash
pip install -r requirements.txt
pip install -r requirements-app.txt
```

**3. 下载权重文件**

在我们的[Release](https://github.com/Zeyi-Lin/HivisionIDPhotos/releases/tag/pretrained-model)下载权重文件`hivision_modnet.onnx` (24.7MB)，存到项目的`hivision/creator/weights`目录下。

拓展抠图模型权重（均放到`hivision/creator/weights`目录下）：
- modnet_photographic_portrait_matting.onnx: [MODNet](https://github.com/ZHKKKe/MODNet)官方权重，[下载](https://drive.google.com/drive/folders/1umYmlCulvIFNaqPjwod1SayFmSRHziyR)


<br>

# 🚀 运行 Gradio Demo

```bash
python app.py
```

运行程序将生成一个本地 Web 页面，在页面中可完成证件照的操作与交互。

<br>

# 🚀 Python 推理

核心参数：

- `-i`: 输入图像路径
- `-o`: 保存图像路径
- `-t`: 推理类型，有idphoto、human_matting、add_background、generate_layout_photos可选
- `--matting_model`: 人像抠图模型权重选择，可选`hivision_modnet`、`modnet_photographic_portrait_matting`

更多参数可通过`python inference.py --help`查看

## 1. 证件照制作

输入 1 张照片，获得 1 张标准证件照和 1 张高清证件照的 4 通道透明 png

```python
python inference.py -i demo/images/test.jpg -o ./idphoto.png --height 413 --width 295
```

## 2. 人像抠图

```python
python inference.py -i -t human_matting demo/images/test.jpg -o ./idphoto_matting.png --matting_model hivision_modnet
```

## 3. 透明图增加底色

输入 1 张 4 通道透明 png，获得 1 张增加了底色的图像）

```python
python inference.py -t add_background -i ./idphoto.png -o ./idhoto_ab.jpg  -c 4f83ce -k 30 -r 1
```

## 4. 得到六寸排版照

输入 1 张 3 通道照片，获得 1 张六寸排版照

```python
python inference.py -t generate_layout_photos -i ./idhoto_ab.jpg -o ./idhoto_layout.jpg  --height 413 --width 295 -k 200
```

<br>

# ⚡️ 部署 API 服务

## 启动后端

```
python deploy_api.py
```


## 请求 API 服务 - Python Request

> 请求方式请参考 [API 文档](docs/api_CN.md)，含 [cURL](docs/api_CN.md#curl-请求示例)、[Python](docs/api_CN.md#python-请求示例)、[Java](docs/api_CN.md#java-请求示例)、[Javascript](docs/api_CN.md#javascript-请求示例) 请求示例。

### 1. 证件照制作

输入 1 张照片，获得 1 张标准证件照和 1 张高清证件照的 4 通道透明 png

```python
import requests

url = "http://127.0.0.1:8080/idphoto"
input_image_path = "demo/images/test.jpg"

files = {"input_image": open(input_image_path, "rb")}
data = {"height": 413, "width": 295}

response = requests.post(url, files=files, data=data).json()

# response为一个json格式字典，包含status、image_base64_standard和image_base64_hd三项
print(response)

```

### 2. 增加底色

输入 1 张 4 通道透明 png，获得 1 张增加了底色的图像

```python
import requests

url = "http://127.0.0.1:8080/add_background"
input_image_path = "test.png"

files = {"input_image": open(input_image_path, "rb")}
data = {"color": '638cce', 'kb': None}

response = requests.post(url, files=files, data=data).json()

# response为一个json格式字典，包含status和image_base64
print(response)
```

### 3. 得到六寸排版照

输入 1 张 3 通道照片，获得 1 张六寸排版照

```python
import requests

url = "http://127.0.0.1:8080/generate_layout_photos"
input_image_path = "test.jpg"

files = {"input_image": open(input_image_path, "rb")}
data = {"height": 413, "width": 295, "kb": 200}

response = requests.post(url, files=files, data=data).json()

# response为一个json格式字典，包含status和image_base64
print(response)
```

<br>

# 🐳 Docker 部署

## 1. 拉取或构建镜像

> 以下方式三选一

**方式一：拉取镜像：**

```bash
docker pull linzeyi/hivision_idphotos
docker tag linzeyi/hivision_idphotos hivision_idphotos
```

**方式二：Dockrfile 直接构建镜像：**

在确保将模型权重文件[hivision_modnet.onnx](https://github.com/Zeyi-Lin/HivisionIDPhotos/releases/tag/pretrained-model)放到`hivision/creator/weights`下后，在项目根目录执行：

```bash
docker build -t hivision_idphotos .
```

**方式三：Docker compose 构建：**

确保将模型权重文件 [hivision_modnet.onnx](https://github.com/Zeyi-Lin/HivisionIDPhotos/releases/tag/pretrained-model) 放在`hivision/creator/weights`下后，在项目根目录下执行：

```bash
docker compose build
```

## 2. 运行服务

**启动 Gradio Demo 服务**

运行下面的命令，在你的本地访问 [http://127.0.0.1:7860](http://127.0.0.1:7860/) 即可使用。

```bash
docker run -p 7860:7860 hivision_idphotos
```

**启动 API 后端服务**

```bash
docker run -p 8080:8080 hivision_idphotos python3 deploy_api.py
```

**两个服务同时启动**

```bash
docker compose up -d
```

<br>

# 🌲 友情链接

- [HivisionIDPhotos-windows-GUI](https://github.com/zhaoyun0071/HivisionIDPhotos-windows-GUI)

<br>

# 📖 引用项目

1. MTCNN:

```bibtex
@software{ipazc_mtcnn_2021,
    author = {ipazc},
    title = {{MTCNN}},
    url = {https://github.com/ipazc/mtcnn},
    year = {2021},
    publisher = {GitHub}
}
```

2. ModNet:

```bibtex
@software{zhkkke_modnet_2021,
    author = {ZHKKKe},
    title = {{ModNet}},
    url = {https://github.com/ZHKKKe/MODNet},
    year = {2021},
    publisher = {GitHub}
}
```

<br>

# 💻 开发小贴士

**1. 如何修改预设尺寸？**

修改[size_list_CN.csv](demo/size_list_CN.csv)后再次运行 app.py 即可，其中第一列为尺寸名，第二列为高度，第三列为宽度。

<br>

# 📧 联系我们

如果您有任何问题，请发邮件至 zeyi.lin@swanhub.co

<br>

# 贡献者

<a href="https://github.com/Zeyi-Lin/HivisionIDPhotos/graphs/contributors">
  <img src="https://contrib.rocks/image?repo=Zeyi-Lin/HivisionIDPhotos" />
</a>

[Zeyi-Lin](https://github.com/Zeyi-Lin)、[SAKURA-CAT](https://github.com/SAKURA-CAT)、[Feudalman](https://github.com/Feudalman)、[swpfY](https://github.com/swpfY)、[Kaikaikaifang](https://github.com/Kaikaikaifang)、[ShaohonChen](https://github.com/ShaohonChen)、[KashiwaByte](https://github.com/KashiwaByte)

<br>

# StarHistory

[![Star History Chart](https://api.star-history.com/svg?repos=Zeyi-Lin/HivisionIDPhotos&type=Date)](https://star-history.com/#Zeyi-Lin/HivisionIDPhotos&Date)