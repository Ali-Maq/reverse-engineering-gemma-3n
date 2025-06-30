This reverse engineering effort of Gemma 3n almost decrypted the transformer architecture before the official release, using the names of the checkpoint files and matrix dimensions https://lnkd.in/g5A6H7kq

The Gemma 3n Architecture is now out on Hugging Face and all other open-source platforms, and I want to congratulate the folks working on Open Models at Google. While we were working to open-source the model, I was particularly rooting for one reverse-engineering effort that almost decrypted the architecture from the details of the checkpoint files. The reverse engineer missed two crucial details – KV Cache Sharing and Activation Sparsity. In the effort's defense, these two details can’t really be figured out just from the checkpoints. I secretly wanted the reverse-engineering project to win against us!

Now that the model is officially out, here are the major architectural changes and innovations in the Gemma 3n backbone transformer. I’ve also attached the research papers for your convenience:
Matformer: One model, many sizes. The Gemma 3n models are natively elastic between 4B and 2B, allowing for flexible deployment. https://lnkd.in/g7-V2YSu
Altup: Widens the learned representation while only incurring a negligible increase in latency by working on a sub-block of the widened representation at each layer. This leads to more capable models without a significant speed penalty. https://lnkd.in/gWgjaeBP
LAuReL: A generalization of the canonical residual connection, improving model performance and training stability. https://lnkd.in/gawrNVFD
KV Cache Sharing: The KV Cache is reused for the last 20 layers, which is a balance between quality and efficiency. This is a sweet spot between a traditional transformer and YOCO, resulting in faster inference. https://lnkd.in/gyyQgB3w
Activation Sparsity: For large models, activation sparsity reduces computational cost by activating only a small fraction of the model’s parameters for each input. The first 10 layers use 95% activation sparsity in Gemma 3n, making the model more efficient. https://lnkd.in/gibE9y2w
Per-Layer Embeddings (PLE): PLE provides an additional, separate pathway to inject information into each specific layer of the Transformer. Instead of just receiving the main d_model vector, each block also gets a smaller, unique input vector tailored for its position in the stack, enhancing the model's representational power.

I'm incredibly proud of the team and excited to see what the community builds with Gemma 3n!
