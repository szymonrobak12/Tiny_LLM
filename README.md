A small GPT-type language model built from scratch in PyTorch for learning purposes.

A file tiny_llm.ipynb contains two models:
1. Character-level model based on Tiny Shakespeare dataset with hand-written attention head.
Each layer is written the way to make it easier to understand how the model actually works.
It is quick in training and good to see how everything fit together.
2. BPE-token based model trained on tiny piece (around 2.5%) of OpenWebText dataset.
It is slightly larger than Shakespeare model and uses more optimized mechanisms provided by PyTorch (like scaled_dot_product_attention).


Note that this is educational project. The model produces fluent, and rather grammatically correct text,
however it is not coherent over long passages and can't be treated as a chatbot.

More about both models and other things worth mentioning:


1. Details of Tiny_Shakespeare model:

Parameters:
* Tokenization: Character-level (vocab_size -> 65)
* Embedding_dim: 128
* Attention_heads: 4 (hand-written code with core math)
* Transformer_blocks: 4
* Context_length: 128 (characters)
* Batch_size: 64
* Optimizer: AdamW, lr -> 1e-3
* Dropout: 0.2
* Data: https://raw.githubusercontent.com/karpathy/char-rnn/master/data/tinyshakespeare/input.txt
* Train/test split: classic 90/10

Performance:
* training time: a few minutes (on free Google Colab GPU)
* final_test_loss: around 1.4
* final_test_accuracy: 57.6%

'tiny_shakespeare_loss.png' shows all the learning process and model's progress


2. Details of OpenWebText model:

Parameters:
* Tokenization: GPT-2 BPE (tiktoken, vocab_size -> 50 257)
* Embedding_dim: 256
* Attention_heads: 4 (hand-written code with core math)
* Transformer_blocks: 10
* Context_length: 256
* Batch_size: 32
* Optimizer: AdamW, peak lr -> 5e-4, with weight decay 0.01 and LR scheduler -> 500 warmup steps, cosine decay to 10% of peak
* Dropout: No dropout
* Data: around 2.5% (first 2 parquet shards of 80) of OpenWebText dataset -> "Skylion007/openwebtext" 
* Train/test split: classic 90/10

Performance:
* training time: around three hours (on free Google Colab GPU)
* final_test_loss: 4.42
* final_test_perplexity: 82.97

'openwebtext_loss.png' shows all the learning process and model's progress.
This model is prepared to be trained in many sessions (all the progress is saved to 'checkpoints' folder once in 500 training steps).


3. Possible improvement ideas:
* Training model on more data with larger parameters
* Adding temperature and top-k sampling while generating text
* Post-learning/Supervised fine-tuning to obtain chatbot-like behavior

4. Inspiration:
Main inspiration to create the project is taken from 3Blue1Brown YouTube channel, specifically from the "Neural networks" playlist. It was exceedingly helpful in the model implementation and crucial in understanding the whole structure of a LLM. 
