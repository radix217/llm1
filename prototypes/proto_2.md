# Notes

## Takeaways from Qwen 3 0.6B
Qwen3 Technical Report [arXiv:2505.09388v1](https://arxiv.org/pdf/2505.09388)

### Architecture (0.6B)
- Similar to Qwen 2.5 (Yang et al.)
- Dense model, not MoE
- Grouped Query Attention - GQA (Ainslie et al.)
- SwiGLU Activation (Dauphin et al.)
- RoPE for position information (Su et al.)
- RMSNorm (with pre-normalization) (Jiang et al.)
- QK-Norm to attention mechanism for stability (Dehghani et al.), instead of QKV-bias as in Qwen 2

#### Configuration
- Layers : 28
- Heads : 16 (Q) / 8 (KV)
- Tie Embedding : Yes
- Context Length : 32K

### Training
- Pre-trained on 36 Trillion tokens (119 languages and dialects)
- Extended synthetic dataset from domain specific models (Qwen2.5 VL, Math and Coder)
- Three phase Pre-training
    - 30 Trillion tokens, foundation of general knowledge
    - knowledge-intensive data (STEM & coding)
    - long-context data training, to increase context length from 4.096 to 32,768
- Multi-stage post-training
    - stage 1,2 reasoning training
        - long CoT
        - cold-start finetuning
        - RL for maths and coding
    - final 2 stages
        - with and w/o reasoning dataset combined (for flexible handling both modes)
        - general domain RL
        - strong-to-weak distillation**, off-policy and on-policy transfer


