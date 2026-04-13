# Transformers — USP Neural Networks

Lecture materials for the 13/04/2026 class on the Transformer architecture, taught as part of the Neural Networks postgraduate course at the **University of São Paulo (USP)** by **Dr. Ricardo Vilela de Godoy** (USP Robotics Center — CRoB).

The class combines a theory lecture with a hands-on coding challenge in which students implement self-attention, multi-head attention, and a full Transformer block from scratch in PyTorch, then train a mini character-level GPT on Tiny Shakespeare.

---

## What's in this repo

| File | Purpose | Audience |
|---|---|---|
| `Transformers_USP.pptx` | 16-slide lecture deck covering attention, self-attention, multi-head, the Transformer block, decoder masking, training, model families, and applications in robotics | Class projection |
| `Transformers_Colab_Challenge.ipynb` | Student notebook with scaffolded code and three `TODO` blocks to fill in | Students |

---

## Class structure

| Time | Block | Material |
|---|---|---|
| 14:30 – 15:30 | **Part I — Theory** | `Transformers_USP.pptx`|
| 15:30 – 15:50 | Break | — |
| 15:50 – 17:30 | **Part II — Hands-on** | `Transformers_Colab_Challenge.ipynb` |

### Part I — Theory

The lecture moves from motivation (why not RNNs?) through the attention intuition, the input pipeline, the core scaled dot-product operation, multi-head attention, the full Transformer block, decoder masking and cross-attention, training, the three model families (encoder-only / decoder-only / encoder–decoder), and finally the role of Transformers in modern Physical AI and robot learning.

### Part II — Hands-on (Colab)

Students work in pairs to fill in three `TODO` blocks:

1. **`SingleHeadAttention`** — the six-step scaled dot-product recipe with causal masking.
2. **`MultiHeadAttention`** — `nn.ModuleList` of heads, concatenation, output projection `W_O`.
3. **`TransformerBlock`** — pre-norm architecture with residual connections.

The scaffolding (tokenizer, data loader, full model class, training loop, generation, and loss plots) is already provided. After implementing the three pieces, students train a ~2M-parameter MiniGPT on Tiny Shakespeare for 3000 steps (~3 minutes on a Colab T4 GPU) and generate 500 characters of Shakespeare-like prose.

**Pass criterion:** validation loss below ~1.7 (a correct reference run lands around 1.60–1.65).

---

## How to run the Colab challenge

1. Open `Transformers_Colab_Challenge.ipynb` in Google Colab.
2. **Runtime → Change runtime type → T4 GPU** (important — CPU will take hours).
3. Run cells top to bottom. Shape tests after each `TODO` give immediate ✅ / ❌ feedback.
4. Training takes ~3 minutes and should produce a smoothly decreasing loss curve.
5. The final cell generates 500 characters of text seeded with `"ROMEO:"`.

No setup beyond opening the notebook. All dependencies (PyTorch, matplotlib) are preinstalled on Colab.

### Model configuration

| Hyperparameter | Value |
|---|---|
| `block_size` (context length) | 128 |
| `batch_size` | 64 |
| `n_embd` (model dimension) | 192 |
| `n_head` | 6 |
| `n_layer` | 4 |
| `dropout` | 0.1 |
| Optimizer | AdamW, `lr=3e-4` |
| Training steps | 3000 |
| Parameters | ~1.92 M |

---

## Teaching objectives

By the end of the class, a student who completes the challenge should be able to:

- Explain why attention replaced recurrence and what the tradeoffs are.
- Write the scaled dot-product attention formula from memory and justify the `√d_k` scaling.
- Explain what the causal mask does and why training would break without it.
- Implement multi-head attention from scratch without looking anything up.
- Identify the role of residual connections, LayerNorm, and the feed-forward sublayer in the Transformer block.
- Distinguish encoder-only, decoder-only, and encoder–decoder models and match each to appropriate tasks.
- Connect the same architecture to its use in vision (ViT), reinforcement learning (Decision Transformer), and robotics (RT-2, OpenVLA, π0, SmolVLA).

---

## Bonus challenges

There are five extension tasks:

- Replace the learned positional encoding with the original sinusoidal formula from Vaswani et al.
- Rewrite multi-head attention as a single vectorized tensor operation and measure the speedup.
- Sweep temperature and top-k sampling parameters and compare generation quality.
- Swap Tiny Shakespeare for a different dataset (code, Portuguese text, a domain corpus).
- Visualize attention heatmaps from a trained model on a real sentence.

---

## References

The material is inspired by and draws from:

- Vaswani et al. (2017), *Attention Is All You Need* — [arXiv:1706.03762](https://arxiv.org/abs/1706.03762)
- Andrej Karpathy's *Let's build GPT: from scratch, in code, spelled out* — [YouTube](https://www.youtube.com/watch?v=kCc8FmEb1nY) / [nanoGPT](https://github.com/karpathy/nanoGPT)
- Tiny Shakespeare dataset from [karpathy/char-rnn](https://github.com/karpathy/char-rnn)
- Jay Alammar's *The Illustrated Transformer* — [blog post](https://jalammar.github.io/illustrated-transformer/)

For Transformers in robotics specifically:

- Dosovitskiy et al. (2020), *An Image is Worth 16x16 Words* (ViT) — [arXiv:2010.11929](https://arxiv.org/abs/2010.11929)
- Chen et al. (2021), *Decision Transformer* — [arXiv:2106.01345](https://arxiv.org/abs/2106.01345)
- Brohan et al. (2023), *RT-2: Vision-Language-Action Models* — [arXiv:2307.15818](https://arxiv.org/abs/2307.15818)
- Kim et al. (2024), *OpenVLA* — [arXiv:2406.09246](https://arxiv.org/abs/2406.09246)

---

## License and reuse

These materials are released for educational use. If you use them for your own teaching, attribution is appreciated but not required. If you spot a bug, find a better way to explain something, or adapt the materials for a different course, feel free to open an issue or a pull request.

---

## About

**Dr. Ricardo Vilela de Godoy** is a postdoctoral researcher at the **USP Robotics Center (CRoB)** in São Carlos, Brazil, where he leads a locomanipulation research group focused on Physical AI for real-world inspection and automation. His work includes research on human–robot interfaces, shared control, autonomous manipulation, and machine learning for robotics.

USP Neural Networks postgraduate course · São Carlos · April 2026
