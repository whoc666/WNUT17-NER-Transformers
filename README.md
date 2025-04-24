WNUT17-NER-Transformers
项目简介
WNUT17-NER-Transformers 是一个基于WNUT-17数据集的命名实体识别（NER）网页应用。用户可以通过网页界面输入文本，系统将自动识别并高亮显示文本中的实体，例如人名（person）、组织（organization）、地点（location）等。该项目使用DistilBERT模型在WNUT-17数据集上进行微调，模型托管在Hugging Face，网页通过GitHub Pages部署，支持在线使用和本地测试。
项目背景
WNUT-17数据集来源于社交媒体文本，包含多种实体类型，适用于NER任务。本项目旨在通过浏览器端的推理（使用transformers.js）提供一个轻量级的NER工具，方便用户快速体验和测试。
在线演示

在线地址：https://whoc666.github.io/WNUT17-NER-Transformers/
测试示例：
输入：@elon KFC
预期输出：
@elon (B-person)
KFC (B-organization)





功能特点

实体识别：支持识别WNUT-17数据集中的多种实体类型，如人名、组织、地点等。
高亮显示：识别结果以不同颜色高亮显示，便于查看（例如人名为红色，组织为蓝色）。
在线与本地支持：提供在线网页访问，同时支持本地部署以应对网络限制。
轻量级：无需安装复杂环境，直接在浏览器中运行。

模型信息

模型名称：whoc666/wnut17-ner
模型地址：https://huggingface.co/whoc666/wnut17-ner
基础模型：distilbert-base-uncased
训练数据集：WNUT-17数据集，包含社交媒体文本中的实体标注。
任务：Token分类（NER），支持B-person、B-organization、B-location等标签。

使用方法
在线使用

访问在线演示地址：https://whoc666.github.io/WNUT17-NER-Transformers/
在输入框中输入待识别的文本（例如@elon KFC）。
点击“Predict Entities”（预测实体）按钮。
查看输出区域，高亮显示的实体会以不同颜色标注，例如：
人名（B-person）：红色
组织（B-organization）：蓝色
地点（B-location）：绿色



本地测试（适用于网络受限环境）
如果你所在的地区无法访问huggingface.co或cdn.jsdelivr.net，可以按照以下步骤在本地测试：
1. 克隆仓库
git clone https://github.com/whoc666/WNUT17-NER-Transformers.git
cd WNUT17-NER-Transformers

2. 下载依赖文件

下载transformers.js：在Google Colab中运行以下代码：
import requests
url = "https://cdn.jsdelivr.net/npm/@huggingface/transformers@2.7.0/dist/transformers.min.js"
response = requests.get(url)
with open("transformers.min.js", "wb") as f:
    f.write(response.content)
from google.colab import files
files.download("transformers.min.js")

将下载的transformers.min.js放置在仓库根目录。

下载模型文件：在Google Colab中运行以下代码：
from huggingface_hub import snapshot_download
import shutil
snapshot_download(repo_id="whoc666/wnut17-ner", local_dir="./model")
shutil.make_archive("model", "zip", "./model")
from google.colab import files
files.download("model.zip")

解压model.zip，将model目录放置在仓库根目录。


3. 使用本地版本的index.html
确保你的index.html已配置为使用本地文件：

<script src="./transformers.min.js"></script>
model: "./model"

4. 运行本地服务器
python -m http.server 8000

在浏览器中访问http://localhost:8000/index.html，输入文本进行测试。
技术细节

模型：
基于distilbert-base-uncased，在WNUT-17数据集上微调。
任务：命名实体识别（NER），支持WNUT-17标签体系。


前端：
使用HTML、CSS和JavaScript开发。
通过transformers.js在浏览器中运行模型推理。


部署：
网页托管在GitHub Pages，地址为https://whoc666.github.io/WNUT17-NER-Transformers/。


依赖：
transformers.js（在线版本通过CDN加载：https://cdn.jsdelivr.net/npm/@huggingface/transformers@2.7.0/dist/transformers.min.js）。
模型文件（在线版本从whoc666/wnut17-ner加载）。



项目结构
WNUT17-NER-Transformers/
│
├── index.html           # 在线版本网页文件
├── transformers.min.js  # 本地版本所需的transformers.js文件（可选）
├── model/               # 本地版本所需的模型文件（可选）
│   ├── config.json
│   ├── model.safetensors
│   ├── tokenizer.json
│   └── ...
└── README.md            # 项目说明文件

常见问题解答（FAQ）
1. 为什么在线网页无法加载？

可能原因：你的网络无法访问huggingface.co或cdn.jsdelivr.net（例如在中国大陆地区）。
解决方法：
使用VPN切换到无网络限制的地区（例如美国或新加坡）。
按照“本地测试”步骤，将依赖文件本地化。



2. 模型识别结果不准确怎么办？

可能原因：WNUT-17数据集主要针对社交媒体文本，模型可能不适用于其他领域（例如正式文档）。
解决方法：
尝试使用社交媒体风格的文本（例如@elon KFC）。
对比其他NER模型（例如dslim/bert-base-NER）的预测结果。



3. 如何查看错误信息？

按F12打开浏览器开发者工具，切换到“Console”选项卡，查看详细错误信息（例如“Cannot connect to Hugging Face model repository”）。

贡献指南
欢迎对本项目提出改进建议或贡献代码！以下是贡献步骤：

Fork本仓库。
创建你的分支（git checkout -b feature/YourFeature）。
提交更改（git commit -m "Add your feature"）。
推送到分支（git push origin feature/YourFeature）。
创建Pull Request，说明你的更改内容。

改进方向

优化模型性能：尝试其他预训练模型（如BERT、RoBERTa）。
增强界面功能：添加批量处理、实体过滤等功能。
扩展数据集：支持更多领域的NER任务。

联系方式

作者：whoc666
GitHub：https://github.com/whoc666
问题反馈：请在GitHub仓库提交Issue，我会尽快回复。

致谢

感谢Hugging Face提供的transformers.js和模型托管服务。
感谢WNUT-17数据集作者提供的开源数据。
感谢GitHub Pages提供的免费网页托管。

许可证
本项目采用MIT许可证，详情请见LICENSE文件。
