A small GPT-type language model built from scratch in PyTorch for learning purposes.

A file tiny_llm.ipynb contains two models:
1. Character-level model based on Tiny Shakespeare dataset with hand-written attention head.
Each layer is written the way to make it easier to understend how the model actually works.
It is quick in training and good to see how everything fit together.
2. BPE-token based model trained on tiny piece (around 2.5%) of OpenWebText dataset.
It is slightly larger that Shakespeare model and uses more optimized mechanisms provided by PyTorch (like scaled_dot_product_attention).

Note that this is educational project. The model produces fluent, and rather gramatically correct text,
however it is not coherent over long pasages and can't be treated as a chatbot.
