---
layout: post
title: 【Haystack 1】- Installation 
date: 2023-09-11 20:40:16
description: 
tags: AI
giscus_comments: true
featured: false
pretty_table: true
toc:
    sidebar: left
---
Hello world! :smile:

# How to cooperate with LLM?

1. 相关技术
    - **RAG**:结合信息检索与模型生成的方法。通过检索相关文档来辅助生成答案或内容。**从外部知识库中检索信息、结合大模型生成更精准的答案。**
    - **Prompt Engineering**:给模型提供一个合适的输入提示，模型根据**该提示生成相应的输出。**通过设计不同的 Prompt，可以显著影响大模型的行为。
    - **Fine-Tuning**:在已有的大模型基础上进行再训练，使其适应特定的任务。**在小规模的数据集上进行微调**，而不需要重新训练整个模型。
    - Zero-shot & Few-shot Learning:模型不需要针对新任务的数据进行训练就可以完成任务，Few-shot 则是在非常少的数据样本上进行训练。
    - Distillation（模型蒸馏）:通过将大型模型的知识压缩到较小模型中，从而保持性能但减少计算成本和模型大小
    - Active Learning:智能地选择数据进行标注的技术，模型会主动选择不确定的数据来减少标注成本。
    - Transfer Learning:将大模型在某个领域学习到的知识转移到另一个领域，减少新任务所需的数据和计算量。

2. 相关框架

<table id="table" data-toggle="table" data-url="{{ 'assets/json/rag_data/table_1.json' | relative_url }}">
  <thead>
    <tr>
      <th data-field="name">Name</th>
      <th data-field="technology">Technology</th>
      <th data-field="description">Description</th>
      <th data-field="link">Link</th>
    </tr>
  </thead>
</table>


# What's RAG & ?
