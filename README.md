# A Large-Scale Benchmark for Vietnamese Sentence Paraphrases

## Introduction

Paraphrasing involves rewriting sentences with different words while preserving the original meaning. It is a vital technique in NLP, supporting various tasks such as Question Answering, Information Retrieval, Machine Translation, and Chatbots. However, Vietnamese remains a low-resource language, and existing paraphrase resources mostly focus on English or contain only small, often automatically translated Vietnamese data.

<p align="center">
  <img src=".resources/sample.png" />
</p>

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

## Models Used in Experiments

The models used in our experiments can be found at [LINK](https://huggingface.co/collections/ngwgsang/visp-66ec240d6865fea132a3cb98).  
Below is a simple description of how we used them:

```python
import torch
from transformers import pipeline

# Set device to GPU if available, else fallback to CPU
device = 0 if torch.cuda.is_available() else -1

# Choose a fine-tuned model for ViSP paraphrasing
model_name = "ngwgsang/vit5-base-visp-s1"  # You can change to any other ViSP model

# Initialize the text2text generation pipeline
paraphraser = pipeline(
    "text2text-generation",
    model=model_name,
    tokenizer=model_name,
    device=device
)

# Input sentence for paraphrasing
sentence = "Hạnh phúc là khi ta biết đủ với những gì mình đang có."

# Prepend task prefix as expected by the model
prompt = f"sentence-paraphrase: {sentence}"

# Run the model to generate paraphrases
outputs = paraphraser(
    prompt,
    max_length=96,
    num_beams=5,
    do_sample=True,
    # temperature=0.9,
    # top_k=50,
    # top_p=0.95,
    num_return_sequences=3,
    early_stopping=True
)

# Display input and generated paraphrases
print(f"Input: {sentence}\n")
print("Generated Paraphrases:")
for i, o in enumerate(outputs, 1):
    print(f"{i}. {o['generated_text']}")

# >>> Input: Hạnh phúc là khi ta biết đủ với những gì mình đang có.
# Generated Paraphrases:
# 1. Hạnh phúc là khi ta biết trân trọng những gì mình đang có.
# 2. Hạnh phúc là khi ta biết hài lòng với những gì mình đang có.
# 3. Hạnh phúc là khi ta biết đủ với những gì mình đang có.
```

## Citation

Details of the dataset construction and experimental results can be found in our [NAACL 2025](https://aclanthology.org/2025.findings-naacl.59/) paper:

Please CITE our paper when ViSP is used to help produce published results or is incorporated into other software.
```
@inproceedings{nguyen-nguyen-2025-large,
    title = "A Large-Scale Benchmark for {V}ietnamese Sentence Paraphrases",
    author = "Nguyen, Sang Quang  and
      Nguyen, Kiet Van",
    editor = "Chiruzzo, Luis  and
      Ritter, Alan  and
      Wang, Lu",
    booktitle = "Findings of the Association for Computational Linguistics: NAACL 2025",
    month = apr,
    year = "2025",
    address = "Albuquerque, New Mexico",
    publisher = "Association for Computational Linguistics",
    url = "https://aclanthology.org/2025.findings-naacl.59/",
    pages = "1045--1060",
    ISBN = "979-8-89176-195-7",
    abstract = "This paper presents ViSP, a high-quality Vietnamese dataset for sentence paraphrasing, consisting of 1.2M original{--}paraphrase pairs collected from various domains. The dataset was constructed using a hybrid approach that combines automatic paraphrase generation with manual evaluation to ensure high quality. We conducted experiments using methods such as back-translation, EDA, and baseline models like BART and T5, as well as large language models (LLMs), including GPT-4o, Gemini-1.5, Aya, Qwen-2.5, and Meta-Llama-3.1 variants. To the best of our knowledge, this is the first large-scale study on Vietnamese paraphrasing. We hope that our dataset and findings will serve as a valuable foundation for future research and applications in Vietnamese paraphrase tasks. The dataset is available for research purposes at \url{https://github.com/ngwgsang/ViSP}."
}
```

Please follow this [LINK](https://github.com/ngwgsang/ViSP/tree/main/data) to download the ViSP dataset. By downloading this dataset, USER agrees:
- to use the dataset for research or educational purposes only.
- to cite our NAACL 2025 paper "A Large-Scale Benchmark for Vietnamese Sentence Paraphrases" whenever the dataset is used to help produce published results.
