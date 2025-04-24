WNUT17-NER-Transformers

基于WNUT-17数据集和Hugging Face Transformers的命名实体识别（NER）项目，在Google Colab上实现。

项目概述

本项目使用DistilBERT模型在WNUT-17数据集上进行命名实体识别（NER）任务。项目包括数据预处理、模型训练、评估和推理的完整流程，适合初学者学习NER任务和Hugging Face工具的使用。

功能





数据集: WNUT-17（社交媒体文本的NER数据集）



模型: DistilBERT（轻量高效的预训练模型）



功能: 数据分词与标签对齐、模型微调、评估指标计算（精确率、召回率、F1分数）、推理示例



环境: Google Colab（支持GPU加速）

快速开始





打开Google Colab，上传NER_WNUT17_Colab.ipynb。



按照笔记本中的步骤逐一运行代码。



确保安装了所需库（transformers, datasets, evaluate, seqeval, torch）。



训练完成后，可使用保存的模型进行推理。

依赖





Python 3.7+



PyTorch



Hugging Face Transformers



Datasets



Evaluate



Seqeval

文件结构





NER_WNUT17_Colab.ipynb: 完整的Colab笔记本，包含所有代码



ner_wnut17_model/: 训练后的模型文件（需运行代码生成）



README.md: 项目说明

使用示例

from transformers import pipeline
ner_pipeline = pipeline("ner", model="./ner_wnut17_model", tokenizer="./ner_wnut17_model")
test_sentence = "Apple Inc. is planning to open a new store in New York."
results = ner_pipeline(test_sentence)
print(results)

贡献

欢迎提交Issue或Pull Request，提出改进建议或新功能！

许可证

MIT License

联系

如有问题，请通过GitHub Issue联系。
