# A Large-Scale Benchmark for Vietnamese Sentence Paraphrases



## Introduction

Paraphrasing involves rewriting sentences with different words while preserving the original meaning. It is a vital technique in NLP, supporting various tasks such as Question Answering, Information Retrieval, Machine Translation, and Chatbots. However, Vietnamese remains a low-resource language, and existing paraphrase resources mostly focus on English or contain only small, often automatically translated Vietnamese data.

ViSP addresses this gap by providing a large-scale dataset of over 1.2 million Vietnamese sentence pairs from diverse topics. Each original sentence is accompanied by multiple paraphrases, all manually verified to ensure quality. We also evaluate various paraphrase generation methods—including rule-based approaches, back translation, and neural models—comparing them against human performance to highlight their strengths and limitations.

We hope ViSP and our empirical study will serve as a foundation for future research and applications in Vietnamese paraphrasing 🙌.

## Dataset

The ViSP dataset consists of 1.2M+ pairs of Vietnamese paraphrased sentences spanning various domains. Each original sentence is accompanied by multiple paraphrased versions, ensuring the semantic meaning is preserved while offering diverse expressions. Note that ViSP is intended primarily for research and analysis in Vietnamese paraphrasing, rather than fine-tuning any single downstream model.

Each ViSP sample has the following format
```json
{
 "id": "fe23d793-7cbd-4ee5-ae56-4973e1784f7d",
 "source": "ViNLI",
 "topic": "science",
 "original": "Sao xung là những ngôi sao neutron đậm đặc, nặng ít nhất gấp 1,4 lần Mặt Trời, thường được hình thành sau sự kiện siêu tân tinh khi một ngôi sao lớn sụp đổ khiến vật chất ở phần lõi bị nén lại.",
 "paraphrases": [
    {
      "para_id": "para-c089633b-5ed9-464a-8a96-67ccf43d5b67",
      "text": "Sao xung được hình thành từ sự sụp đổ của một ngôi sao lớn sau vụ nổ siêu tân tinh, khiến vật chất ở lõi bị nén lại thành một ngôi sao neutron đặc và nặng ít nhất gấp 1,4 lần Mặt Trời.",
    },
    {
      "para_id": "para-15aaa6bb-23e9-43b1-94a6-f0d7fa944ee2",
      "text": "Sao xung là những ngôi sao neutron đặc, nặng hơn Mặt Trời ít nhất 1,4 lần, được tạo thành sau vụ nổ siêu tân tinh, khi một ngôi sao lớn sụp đổ và phần lõi bị nén chặt lại.",
    }
  ]
}
```

## Usages
Details of the dataset construction and experimental results can be found in our [NAACL 2025]() paper:
```
```

Please follow this [LINK]() to download the PhoMT dataset. By downloading this dataset, USER agrees:
- to use the dataset for research or educational purposes only.
- to cite our NAACL 2025 paper "A Large-Scale Benchmark for Vietnamese Sentence Paraphrases" whenever the dataset is used to help produce published results.

