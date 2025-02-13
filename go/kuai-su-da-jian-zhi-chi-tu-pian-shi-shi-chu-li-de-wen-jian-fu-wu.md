---
description: xulin
---

# 🖼️ 快速搭建支持图片实时处理的文件服务

## 使用 slimfiler 构建高效的文件服务器

在现代 Web 开发中，文件管理是一个常见的需求，尤其是**图片**的处理和存储。`slimfiler`是一个用 Go 语言开发的文件服务器，它不仅支持文件的上传、下载和管理，还内置了强大的图片处理功能，例如**缩放**、**裁剪**和**格式转换**。更值得一提的是，`slimfiler`的图片处理功能兼容 `aliyun OSS` 图片处理参数，使得开发者可以轻松迁移或集成现有的图片处理逻辑。本文将介绍如何使用 `slimfiler`构建一个高效的文件服务器，并展示其强大的图片处理功能。

***

### SlimFiler 的核心功能

1. **文件上传与下载** `slimfiler`提供了简单易用的 API 来处理文件的上传和下载，支持多种存储后端（如本地文件系统、云存储等）。
2. **图片处理** `slimfiler`内置了强大的图片处理功能，支持以下操作：
   * 缩放（resize）
   * 裁剪（crop）
   * 格式转换（如将 PNG 转换为 JPG）
   * 旋转（rotate）
   * 水印（watermark）等功能
3. **兼容 Aliyun OSS 参数** `slimfiler`的图片处理参数与阿里云 OSS 图片处理参数完全兼容，这意味着你可以直接使用阿里云 OSS 的图片处理参数来处理图片。
4. **轻量高效** 由于是用 Go 语言开发的，`slimfiler`具有高性能和低资源占用的特点，适合处理高并发的文件请求。

***

### 安装 SlimFiler

要使用 `slimfiler`，首先需要将其安装到你的开发环境中。你可以通过以下步骤安装：

1.  克隆 `slimfiler`的 GitHub 仓库：

    ```
    git clone https://github.com/AndsGo/slimfiler.git
    cd slimfiler
    ```
2.  使用 Go 编译并运行：

    ```
    go build -o slimfiler
    ./slimfiler
    ```
3.  或者直接下载执行包直接运行：

    linux [下载](https://github.com/AndsGo/SlimFiler/releases/download/v1.1.0/slimfiler)

    windows [下载](https://github.com/AndsGo/SlimFiler/releases/download/v1.1.0/slimfiler.exe)

    配置文件 [下载](https://github.com/AndsGo/slimfiler/releases/download/v1.1.0/conf.yaml)

    ```
    slimfiler -f ./conf.yaml
    ```

    or

    ```
    slimfiler.exe -f ./conf.yaml
    ```

***

### 配置 SlimFiler

`slimfiler`的配置文件是一个简单的 YAML 文件。

默认使用本地存储，可以切换成支持S3协议的对象存储，如`minio`,`AWS s3`,`aliyun oss`

```yaml
Name: aigc
Port: 8000
UploadConf:
  MaxImageSize: 33554432  # 32 mb
  MaxVideoSize: 1073741824 # 1gb
  MaxAudioSize: 33554432  # 32mb
  MaxOtherSize: 10485760  # 10 mb
  ServerURL: "" # nginx path
  Node: DiskOptions
  DiskOptions:
    DiskPath: "./data/file/public"
  S3Options:
    Bucket: ""
    Endpoint: ""
    SecretId: ""
    SecretKey: ""
    Region: ""
    Token: ""
    S3ForcePathStyle: true
    DisableSSL: false
PorxyCacheConf:
  MaxCacheSize: 10485760 # 10M
  Node: DiskOptions 
  DiskOptions:
    DiskPath: "./data/cache" # 一般在 /tmp 下
  S3Options:
    Bucket: ""
    Endpoint: ""
    SecretId: ""
    SecretKey: ""
    Region: ""
    Token: ""
    S3ForcePathStyle: true
    DisableSSL: false
Db:
  Path: ./data/file/db/slimfiler.db
  BuketName: "slimfiler" # difualt bucket name
Log:
  FileName: slimfilerLog
  Path: ./data/logs
  Level: info
  Compress: false
  KeepDays: 7
  StackCoolDownMillis: 100
```

### 使用 SlimFiler 处理文件

#### 1. 文件上传

使用 `slimfiler`上传文件非常简单。以下是一个使用 `curl` 上传文件的示例：

```sh
curl -X POST -F "file=@/path/to/your/image.jpg" http://localhost:8080/upload
```

上传成功后，`slimfiler` 会返回文件`url`，用于后续的文件访问和处理。

#### 2. 文件查看/下载

通过文件的唯一标识符，可以直接下载文件：

```sh
curl -O http://127.0.0.1:8080/data/test/2025-02-07/987cb8c4-f7f8-4b1e-940a-f9dee03e6ec8.jpg
```

#### 3. 文件代理

代理 将需要代理的`url`追加到 `/proxy/`后面

```
http://127.0.0.1:8000/proxy/https://raw.githubusercontent.com/AndsGo/imageprocess/refs/heads/main/examples/example.jpg
```

文件代理支持缓存，可以用于简单的内网CDN加速。

例如上面的链接[https://raw.githubusercontent.com/AndsGo/imageprocess/refs/heads/main/examples/example.jpg](https://raw.githubusercontent.com/AndsGo/imageprocess/refs/heads/main/examples/example.jpg)

我直接访问需要 2s,代理缓存后，

<figure><img src="../.gitbook/assets/image-20250212210515191.png" alt=""><figcaption></figcaption></figure>

再重新访问只需要38ms：

<figure><img src="../.gitbook/assets/image-20250212210526283.png" alt=""><figcaption></figcaption></figure>

#### 4. 图片处理参数

图片处理依赖[imageprocess库](https://github.com/AndsGo/imageprocess),图片查看和代理都支持图片压缩。 图片处理兼容 `aliyun oss` 的图片处理，在url后面添加参数`x-oss-process`即可。支持图片格式：`WEBP`,`JPG`,`JPEG`,`PNG`,`BMP`,`TIFF`,`GIF`。文件查看/下载 和 文件代理都支持图片处理。

以下是一些常见的图片处理示例：

*   **缩放图片** 将图片宽度调整为 300px，高度按比例缩放：

    ```
    ?x-oss-process=image/resize,w_300
    ```
*   **裁剪图片** 将图片裁剪为 200x200 的大小：

    ```
    ?x-oss-process=image/crop,w_200,h_200
    ```
*   **格式转换** 将图片转换为 `webp`格式, `webp`作为新一代图片格式体积会变小不少：

    ```
    ?x-oss-process=image/format,webp
    ```
*   **添加水印** 在图片右下角添加文字水印：

    ```
    ?x-oss-process=image/watermark,text_SlimFiler,color_FFFFFF,size_20,g_se,x_10,y_10
    ```

这些参数与阿里云 OSS 完全兼容，因此你可以直接将现有的 OSS 图片处理逻辑迁移到 `slimfiler`。

图片处理功能使用

***

### 总结

`flimfiler`是一个功能简单且易于使用的文件服务器，特别适合需要处理图片的 Web 应用。它支持文件的上传、下载和管理，并内置了与阿里云 OSS 兼容的图片处理功能。通过简单的配置和灵活的 API，`flimfiler`可以帮助开发者快速构建高效的文件服务。

如果你正在寻找一个轻量级且支持图片实时处理的的文件服务器，`slimfiler` 绝对是一个值得尝试的工具。更多详细信息，访问 [GitHub 仓库](https://github.com/AndsGo/slimfiler)。

\
