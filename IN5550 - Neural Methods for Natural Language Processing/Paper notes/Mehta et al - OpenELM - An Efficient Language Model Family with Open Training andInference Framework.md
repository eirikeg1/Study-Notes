
* [Mehta et al 2019](https://arxiv.org/pdf/2404.14619)

## Abstract
*The reproducibility and transparency of large language models are crucial for advancing open research, ensuring the trustworthiness of results, and enabling investigations into data and model biases, as well as potential risks. To this end, we release OpenELM, a state-of-the-art open language model. OpenELM uses a layer-wise scaling strategy to efficiently allocate parameters within each layer of the transformer model, leading to enhanced accuracy. For example, with a parameter budget of approximately one billion parameters, OpenELM exhibits a 2.36% improvement in accuracy compared to OLMo while requiring 2× fewer pre-training tokens. Diverging from prior practices that only provide model weights and inference code, and pre-train on private datasets, our release includes the complete framework for training and evaluation of the language model on publicly available datasets, including training logs, multiple checkpoints, and pre-training configurations. We also release code to convert models to MLX library for inference and fine-tuning on Apple devices. This comprehensive release aims to empower and strengthen the open research community, paving the way for future open research endeavors. Our source code along with pre-trained model weights and training recipes is available at https://github. com/apple/corenet. Additionally, OpenELM models can be found on HuggingFace at: https : / / huggingface.co/apple/OpenELM*


# Main takeaways

## Architecture
* No bias in feed forward layers
* ROPE positional embeddings
* Grouped Query Attention
* Replace Feed Forward Network with SwiFLU FFN
* Use Flash attention for computing the scaled dot product attention
* Use LLama tokenizer



