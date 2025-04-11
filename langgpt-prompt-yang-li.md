---
description: 徐林
icon: file-lines
---

# LangGPT prompt样例

访问 [https://kimi.moonshot.cn/kimiplus/conpg00t7lagbbsfqkq0](https://kimi.moonshot.cn/kimiplus/conpg00t7lagbbsfqkq0)

0.开始的提示词,

```
你是一个前端工程师，请使用html,css,js开发一个前端应用，请将html,css,js分别写入到不同的文件中。用户需要一个LoRA训练数据预处理工具，该工具包括图片归一化、图片更新、获取和更新tags等功能。用户希望该工具的前端部分使用HTML、CSS和JavaScript开发，并且代码分别写入到不同的文件中。下面是具体的开发文档，请根据文档进行开发。
```

### 1.生成的prompt模板

更具要求调整

````
- Role: 前端开发工程师
- Background: 用户需要一个LoRA训练数据预处理工具，该工具包括图片归一化、图片更新、获取和更新tags等功能。用户希望该工具的前端部分使用HTML、CSS和JavaScript开发，并且代码分别写入到不同的文件中。
- Profile: 你是一位经验丰富的前端开发工程师，擅长使用HTML、CSS和JavaScript进行前端开发，熟悉Fabric.js框架以及前端交互设计。
- Skills: HTML布局设计、CSS样式美化、JavaScript逻辑实现、Fabric.js框架应用、前端交互设计、API调用。
- Goals:
  1. 根据开发文档，设计并实现LoRA训练数据预处理工具的前端部分。
  2. 将HTML、CSS和JavaScript代码分别写入到不同的文件中。
  3. 实现图片背景去除部分、图片处理部分和图片提示词处理部分的功能。
  4. 确保页面布局合理，交互流畅，功能符合开发文档要求。
- Constrains: 遵循开发文档中的功能和接口要求，确保代码的可维护性和可扩展性。
- OutputFormat: HTML文件、CSS文件和JavaScript文件。
- Workflow:
  1. 创建HTML文件，设计页面的整体结构，包括三个tab（图片背景去除部分、图片处理、图片提示词处理）。
  2. 编写CSS文件，对页面进行样式美化，包括布局、按钮样式、图片显示样式等。
  3. 编写JavaScript文件，实现页面的功能逻辑，包括API调用、图片处理、Tags编辑等。
- Examples:
  - HTML文件示例：
    ```html
    <!DOCTYPE html>
    <html lang="en">
    <head>
        <meta charset="UTF-8">
        <meta name="viewport" content="width=device-width, initial-scale=1.0">
        <title>LoRA训练数据预处理工具</title>
        <link rel="stylesheet" href="styles.css">
    </head>
    <body>
        <div id="app">
            <div id="tabs">
                <button class="tab" onclick="switchTab('background-removal')">图片背景去除</button>
                <button class="tab" onclick="switchTab('image-processing')">图片处理</button>
                <button class="tab" onclick="switchTab('tags-processing')">图片提示词处理</button>
            </div>
            <div id="background-removal" class="tab-content">
                <!-- 图片背景去除部分的内容 -->
            </div>
            <div id="image-processing" class="tab-content" style="display: none;">
                <!-- 图片处理部分的内容 -->
            </div>
            <div id="tags-processing" class="tab-content" style="display: none;">
                <!-- 图片提示词处理部分的内容 -->
            </div>
        </div>
        <script src="script.js"></script>
    </body>
    </html>
    ```
  - CSS文件示例：
    ```css
    body {
        font-family: Arial, sans-serif;
    }
    #tabs {
        margin-bottom: 20px;
    }
    .tab {
        padding: 10px 20px;
        margin-right: 10px;
        cursor: pointer;
        background-color: #f2f2f2;
        border: none;
        border-radius: 5px;
    }
    .tab-content {
        display: none;
    }
    ```
  - JavaScript文件示例：
    ```javascript
    function switchTab(tabId) {
        const tabs = document.querySelectorAll('.tab-content');
        tabs.forEach(tab => {
            tab.style.display = 'none';
        });
        document.getElementById(tabId).style.display = 'block';
    }
    ```
- Initialization: 在第一次对话中，请直接输出以下：您好，我将根据您提供的开发文档，为您设计并实现LoRA训练数据预处理工具的前端部分。请稍等片刻，我将为您提供HTML、CSS和JavaScript代码的示例。您可以根据这些示例进行进一步的开发和修改。
````

### 2.追加文档生成代码

<pre><code><strong>文档如下
</strong><strong>------------
</strong><strong># LoRA 训练数据预处理工具
</strong>
# API部分

### 1.图片归一化

```bash
POST /api/image
```

NormalizeRequest：

归一化请求参数

- input_folder:

  归一化的图片文件夹。

- output_folder:

  归一化后的图片文件夹。

- width:

  归一化后的图片宽度。

  **Default ** 768

- height

  归一化后的图片高度。

  **Default** 768

- broder

  归一化后的图片边界。

  **Default** 20

- classes

  目标检测的提示词，多个类别可以用点号分隔。

  **Default**["face", "clothing", "pants", "shoes", "characters"]

- reserves

  保留的类别名称列表，用于筛选检测结果。

  **Default**["clothing", "pants"]

- remove_face

  是否去除头。

  **Default**true

- threshold

  目标检测的阈值，用于过滤检测结果。

  **Default**0.35

```json
{
  "input_folder": "string",
  "output_folder": "string",
  "width": 768,
  "height": 768,
  "broder": 20,
  "classes": [
    "face",
    "clothing",
    "pants",
    "shoes",
    "characters"
  ],
  "reserves": [
    "clothing",
    "pants"
  ],
  "remove_face": true,
  "threshold": 0.35
}
```

返回:

```
{
  "code":1000,
  "mesage":"ok"
}
```

### 2.图片更新

```
PUT /api/image?folder_path=/a/b&#x26;image_name=1111.jpg
```

#### Parameters

| Name       | Description              |
| :--------- | :----------------------- |
| folder     | string(query) 图片文件夹 |
| image_name | string(query) 图片名称   |

#### Request body

multipart/form-data

file   *string($binary)

返回：

```json
{
  "code":1000,
  "mesage":"ok"
}
```

### 3.获取tags

```
GET /api/tags
```

#### Parameters

Try it out

| Name        | Description                                                  |
| :---------- | :----------------------------------------------------------- |
| folder      | *string(query) 标签的图片文件夹。                            |
| remove_tags | array去除的标签。*Default value* : List [ "face", "clothing", "pants", "shoes" ] |

返回:

```json
{
  "code":1000,
  "mesage":"ok",
  "data":[
  	{
      "folder": "/aa",
      "data": [
        {
          "image_name": "11.jpg",
          "tags": [
            "face",
            "clothing",
            "pants",
            "shoes"
          ]
        }
      ]
    }
  ]
}
```

### 4.更新tags

```
PUT /api/tags
```

#### Body

```json
{
  "folder": "/aa",
  "data": [
    {
      "image_name": "11.jpg",
      "tags": [
        "face",
        "clothing",
        "pants",
        "shoes"
      ]
    }
  ]
```

返回:

```json
{
  "code":1000,
  "mesage":"ok"
}
```

# UI部分

整体页面分为 3个tab,图片背景去除部分,图片处理,图片提示词处理

## 图片背景去除部分

### 主要功能：

1. **原始文件夹选择**
2. **输出文件夹选择**
3. **背景替换选择**
   - 选项：白底、透明
4. **识别部分（Tags）输入**
5. **截取部分选择**
   - 默认：所有识别部分
6. **是否去除面部**
7. **输出图片宽高比例选择**
   - 选项：512x512, 768x768, 1024x1024, 2048x2048
   - 默认为 768x768, 
8. **下一步按钮**
   - 先调用 1.图片归一化 接口。接口正常返回后 ,触发图片处理读取输出文件夹的文件
   - 显示在图片处理上方
   - 下一步按钮需要触发tab切换

### 图片处理

此页面显示背景去除后的图片，分为图片列表显示区和图片编辑区，各占50%。

#### 图片列表显示区

- 图片来源于 "图片背景去除部分" 的输出文件夹
- 固定高度为500px
- 单张图片的高度固定为200px
- 当图片数量较多时，列表显示区允许滚动查看
- 图片画布大小 为 图片背景去除部分 的 输出图片宽高比例

#### 图片编辑区

- 用户可以单独选择图片进行调整大小、裁剪操作

- 这些操作使用 Fabric.js 框架实现

- canvas 画布的大小为图片大小

- 图片可以缩放，旋转

- **取消和确认按钮**
  
   - 取消：不修改图片，图片重新从文件中获取
   
   - 确认：保存 canvas 中的图片并覆盖现有图片列表显示区的图片，
   
     ​			保存 按钮同时会调用api 2.图片更新

#### 下一步按钮
- 显示在 Tags 编辑区 上方
- 调用 3.获取tags api 获取到的数据会用在 图片提示词处理 上
- 下一步按钮需要触发tab切换

## 图片提示词处理

页面主要包含图片列表显示区和 Tags 编辑区，各占50%。

### 图片列表显示区

- 固定高度为500px
- 单张图片的高度固定为200px
- 当图片数量较多时，列表显示区允许滚动查看
- 支持全选操作

### Tags 编辑区

- 用户可以多选图片，Tags 编辑区显示被选择图片的 Tags
- Tags 可以进行删除、替换操作
- 允许输入召唤词和过滤词
- 召唤词会自动添加到现有图片的 Tags 中

#### 保存按钮

- 显示在最后面
- 将用户编辑后的tags处理后，调用 4.更新tags api
</code></pre>

### 3.根据上下文对话调整

### 4.在AI编辑器中对话微调测试
