# AI Engineering: 12-Week Depth-Through-Building Roadmap

> **Goal:** Develop first-principles understanding of language models while building credible, public evidence of AI-engineering ability.
>
> **Time budget:** 10 required hours per week, with up to 10 optional extension hours.
>
> **Hardware:** MacBook M1 Pro with 16 GB unified memory. Use free Colab/Kaggle GPUs when CUDA is necessary. Spend up to $20 on cloud GPU time only when free options cannot complete an essential experiment.

## How to use this roadmap

- Check an item only when you can explain or reproduce it without blindly following the resource.
- **Required** resources are part of the core path.
- **Reference** resources are for implementation details or clarification.
- **Optional** items are for weeks when 15–20 hours are available.
- Keep one learning log containing questions, experiment results, failures, and weekly summaries.
- Each week must end with code, measurements, tests, or an explanation—not only consumed content.

## Overall progress

- [ ] Week 1 — Tensors, losses, gradient descent, and generalization
- [ ] Week 2 — Backpropagation and an autograd engine
- [ ] Week 3 — PyTorch training without hidden abstractions
- [ ] Week 4 — Language modeling and tokenization
- [ ] Week 5 — Self-attention and the transformer
- [ ] Week 6 — Train and analyze a tiny transformer
- [ ] Week 7 — Open models, Hugging Face, and baseline evaluation
- [ ] Week 8 — Supervised fine-tuning, LoRA, and QLoRA
- [ ] Week 9 — Quantization theory and benchmarking
- [ ] Week 10 — Product-specific evaluation and capstone design
- [ ] Week 11 — Serving, streaming, performance, and observability
- [ ] Week 12 — Final evaluation, release, and public explanation

## Major milestones

- [ ] Implement gradient descent and gradient checking with NumPy
- [ ] Implement a scalar autograd engine and MLP
- [ ] Build a reusable PyTorch training loop
- [ ] Implement and train a tiny GPT-style language model
- [ ] Create a baseline evaluation harness for an open model
- [ ] Fine-tune an open model with LoRA or QLoRA
- [ ] Quantize and benchmark the model across multiple precisions
- [ ] Build and test a production-style inference service
- [ ] Publish a reproducible capstone, article, and demo

---

# Week 1 — Tensors, losses, gradient descent, and generalization

## Learn: tensors, dimensions, broadcasting, and matrix multiplication

### Required resources

- [x] Complete [PyTorch: Tensors tutorial](https://docs.pytorch.org/tutorials/beginner/blitz/tensor_tutorial.html)
- [ ] Read [PyTorch: Broadcasting semantics](https://docs.pytorch.org/docs/stable/notes/broadcasting.html)
- [ ] Read the dimensional behavior in [`torch.matmul`](https://docs.pytorch.org/docs/stable/generated/torch.matmul.html)

### Exercises

- [x] Predict the result shape of `(B, D) @ (D, H)` before running it
- [x] Predict the result shape of `(B, T, D) @ (D, H)`
- [x] Predict the result shape of `(B, T, D) @ (B, D, H)`
- [x] Predict the result shape of `(B, T, D) + (D,)`
- [x] Predict the result shape of `(B, T, D) + (T, D)`
- [ ] Create at least three intentionally invalid shape combinations and explain their errors

## Learn: loss functions, gradient descent, and learning rates

### Required resources

- [ ] Watch [3Blue1Brown: Gradient descent, how neural networks learn](https://www.youtube.com/watch?v=IHZwWFHWa-w)
- [ ] Read [Google ML Crash Course: Gradient descent](https://developers.google.com/machine-learning/crash-course/reducing-loss/gradient-descent)
- [ ] Read [Google ML Crash Course: Learning rate and hyperparameters](https://developers.google.com/machine-learning/crash-course/linear-regression/hyperparameters)
- [ ] Read [CS231n: Optimization notes](https://cs231n.github.io/optimization-1/) through numerical and analytic gradients

### Reference

- [ ] Consult [Dive into Deep Learning: Linear regression](https://d2l.ai/chapter_linear-regression/linear-regression.html) if the derivation is unclear

## Learn: train, validation, and test splits

- [ ] Read [Google ML Crash Course: Dividing datasets](https://developers.google.com/machine-learning/crash-course/overfitting/dividing-datasets)
- [ ] Read [Made With ML: Splitting datasets](https://madewithml.com/courses/mlops/splitting/)
- [ ] Explain why validation and test sets have different jobs
- [ ] Explain how repeatedly inspecting the test set contaminates it
- [ ] Explain why random splitting can be wrong for temporal or grouped data
- [ ] Define data leakage in your own words and provide one example

## Learn: underfitting, overfitting, bias, and variance

- [ ] Watch [StatQuest: Bias and variance](https://www.youtube.com/watch?v=EuBBz3bI-aA)
- [ ] Read [Google ML Crash Course: Generalization and overfitting](https://developers.google.com/machine-learning/crash-course/overfitting)
- [ ] Complete [Google: Interpreting loss curves](https://developers.google.com/machine-learning/crash-course/overfitting/interpreting-loss-curves)

## Build

Use these only as guidance—not as code to copy:

- [Made With ML: Linear regression from scratch](https://madewithml.com/courses/foundations/linear-regression/)
- [University of Toronto: Linear regression with NumPy](https://www.cs.toronto.edu/~frossard/post/linear_regression/)

Checklist:

- [ ] Generate synthetic linear data with noise
- [ ] Split the data into train, validation, and test sets
- [ ] Implement predictions with NumPy
- [ ] Implement mean squared error
- [ ] Derive and implement gradients for weights and bias
- [ ] Implement gradient descent without PyTorch autograd or `sklearn.linear_model`
- [ ] Implement centered finite-difference gradient checking
- [ ] Test at least five learning rates
- [ ] Plot loss curves for each learning rate
- [ ] Plot the fitted line against the data
- [ ] Use the test set only after choosing the learning rate

## Definition of done

- [ ] Analytic and numerical gradients agree to a small relative error
- [ ] I can explain why a high learning rate diverges
- [ ] I can explain what the validation set changed about my decisions
- [ ] The repository contains reproducible instructions and results

## Publish

- [ ] Write a short note: “What actually happens when the learning rate is too small, too large, or reasonable?”
- [ ] Include the loss curves rather than only describing them

---

# Week 2 — Backpropagation and an autograd engine

## Learn: derivatives, chain rule, computation graphs, and backpropagation

- [ ] Watch [Karpathy: Building micrograd](https://www.youtube.com/watch?v=VMj-3S1tku0)
- [ ] Review the exercises on [Karpathy: Zero to Hero](https://karpathy.ai/zero-to-hero.html)
- [ ] Use [Karpathy’s notebooks](https://github.com/karpathy/nn-zero-to-hero) only to compare after attempting the implementation

## Learn: activation functions and gradient flow

- [ ] Read the sigmoid, tanh, ReLU, initialization, and gradient-flow sections in [CS231n training slides](https://cs231n.stanford.edu/slides/2023/lecture_7.pdf)
- [ ] Explain why saturated sigmoid/tanh units can produce small gradients
- [ ] Explain why a neural network needs nonlinear activation functions

## Learn: numerical gradient checking

- [ ] Read “Gradient Checks” in [CS231n: Learning and Evaluation](https://cs231n.github.io/neural-networks-3/)
- [ ] Implement centered differences rather than one-sided differences
- [ ] Compare gradients using relative error rather than only absolute error

## Build

- [ ] Implement a scalar `Value` type
- [ ] Implement addition and multiplication
- [ ] Implement powers, negation, subtraction, and division
- [ ] Implement `tanh` and ReLU
- [ ] Record graph parents and operations
- [ ] Implement topological sorting
- [ ] Implement reverse-mode automatic differentiation
- [ ] Correctly accumulate gradients at shared graph nodes
- [ ] Implement gradient reset
- [ ] Implement neuron, layer, and MLP abstractions
- [ ] Train the MLP on a tiny binary dataset
- [ ] Compare gradients with an equivalent PyTorch expression

## Tests

- [ ] Test every supported operation independently
- [ ] Test expressions in which one value is used more than once
- [ ] Test finite-difference agreement
- [ ] Test agreement with PyTorch autograd
- [ ] Test that the tiny MLP can overfit its dataset

## Definition of done

- [ ] I can draw the computation graph for one prediction
- [ ] I can explain forward pass versus backward pass
- [ ] I can explain why reverse-mode autodiff is useful for many parameters and one scalar loss
- [ ] My implementation was reconstructed, not copied line-for-line from `micrograd`

## Publish

- [ ] Create a visual explanation of one prediction and its gradient flow

---

# Week 3 — PyTorch training without hidden abstractions

## Learn: datasets, loaders, batching, and shuffling

- [ ] Complete [PyTorch: Datasets and DataLoaders](https://docs.pytorch.org/tutorials/beginner/basics/data_tutorial.html)
- [ ] Read relevant portions of [PyTorch: Custom datasets and data loaders](https://docs.pytorch.org/tutorials/beginner/data_loading_tutorial.html)

## Learn: modules, autograd, losses, optimizers, and checkpoints

Complete these sections of the [PyTorch beginner sequence](https://docs.pytorch.org/tutorials/beginner/basics/intro.html):

- [ ] Tensors
- [ ] Build Model
- [ ] Automatic Differentiation
- [ ] Optimization Loop
- [ ] Save and Load Model
- [ ] Complete [PyTorch: Training with PyTorch](https://docs.pytorch.org/tutorials/beginner/introyt/trainingyt.html)

## Learn: initialization, regularization, and training dynamics

- [ ] Watch “Building makemore Part 3: Activations & Gradients, BatchNorm” from [Zero to Hero](https://karpathy.ai/zero-to-hero.html)
- [ ] Review initialization, regularization, optimization, and learning-rate sections in [CS231n training slides](https://cs231n.stanford.edu/slides/2023/lecture_7.pdf)

## Learn: debugging neural-network training

- [ ] Read all of [Karpathy: A Recipe for Training Neural Networks](https://karpathy.github.io/2019/04/25/recipe/)
- [ ] Turn the article into a reusable debugging checklist

## Learn: reproducibility and tracking

- [ ] Read [PyTorch: Reproducibility](https://docs.pytorch.org/docs/stable/notes/randomness.html)
- [ ] Set Python, NumPy, and PyTorch seeds
- [ ] Choose experiment logging: [W&B quickstart](https://github.com/wandb/wandb#quickstart) or local JSON/CSV

## Build

- [ ] Recreate the Week 2 MLP with PyTorch
- [ ] Create a custom `Dataset`
- [ ] Create train, validation, and test `DataLoader` instances
- [ ] Write an explicit training loop
- [ ] Write a separate evaluation loop
- [ ] Use `model.train()` and `model.eval()` correctly
- [ ] Use `torch.no_grad()` during evaluation
- [ ] Save and load checkpoints
- [ ] Add validation-based best-checkpoint selection
- [ ] Add early stopping
- [ ] Log configurations and metrics
- [ ] Run an SGD-versus-Adam experiment
- [ ] Run a dropout or weight-decay experiment
- [ ] Confirm the model can overfit one tiny fixed batch

## Definition of done

- [ ] Tiny-batch loss approaches zero before full training
- [ ] The test set does not influence checkpoint or hyperparameter selection
- [ ] Every run records seed, optimizer, learning rate, architecture, and results
- [ ] A new checkout can reproduce the training command

---

# Week 4 — Language modeling and tokenization

## Learn: next-token prediction, bigrams, NLL, and sampling

- [ ] Watch [Karpathy: Building makemore](https://www.youtube.com/watch?v=PaCmpygFfXo)
- [ ] Watch relevant sections of [Karpathy: Building makemore Part 2](https://www.youtube.com/watch?v=TCH_1BHY58I)

## Learn: language-model probability and perplexity

- [ ] Read Section 1 of [Stanford CS224N language-model notes](https://web.stanford.edu/class/cs224n/readings/cs224n-2019-notes05-LM_RNN.pdf)
- [ ] Read [Hugging Face: Perplexity of fixed-length models](https://huggingface.co/docs/transformers/en/perplexity)
- [ ] Explain the chain-rule factorization of sequence probability
- [ ] Explain why perplexity is exponentiated average negative log-likelihood
- [ ] Explain why perplexity is not directly comparable across different tokenizers

## Learn: character, word, and subword tokenization

- [ ] Read [Hugging Face: BPE tokenization](https://huggingface.co/docs/course/chapter6/5)
- [ ] Read [Hugging Face: WordPiece](https://huggingface.co/docs/course/main/en/chapter6/6)
- [ ] Read [Hugging Face: Unigram tokenization](https://huggingface.co/learn/llm-course/chapter6/7)
- [ ] Optional: Watch “Let’s build the GPT Tokenizer” in the [Zero to Hero playlist](https://www.youtube.com/playlist?list=PLAqhIrjkxbuWI23v9cThsA9GvCAUhRvKZ)

## Learn: greedy, temperature, top-k, and top-p decoding

- [ ] Read [Hugging Face: Generation strategies](https://huggingface.co/docs/transformers/generation_strategies)

## Build

- [ ] Implement a character tokenizer with `encode` and `decode`
- [ ] Verify `decode(encode(text)) == text` for supported text
- [ ] Implement a count-based bigram language model
- [ ] Implement a neural bigram language model
- [ ] Implement negative log-likelihood evaluation
- [ ] Report validation cross-entropy and perplexity
- [ ] Implement autoregressive generation
- [ ] Add temperature sampling
- [ ] Add top-k sampling
- [ ] Compare character tokenization with a real subword tokenizer
- [ ] Record sequence lengths and vocabulary sizes for both tokenizers

## Definition of done

- [ ] I can derive why cross-entropy corresponds to NLL for next-token prediction
- [ ] I can explain what embeddings replace in the count-based model
- [ ] I can explain how temperature changes the probability distribution

---

# Week 5 — Self-attention and the transformer

## Learn: transformer intuition

- [ ] Read self-attention, multi-head attention, positional encoding, residuals, and normalization in [The Illustrated Transformer](https://jalammar.github.io/illustrated-transformer/)
- [ ] Read decoder-only and masked self-attention in [The Illustrated GPT-2](http://jalammar.github.io/illustrated-gpt2/)

## Learn: queries, keys, values, scaling, and causal masks

Watch [Karpathy: Let’s build GPT from scratch](https://www.youtube.com/watch?v=kCc8FmEb1nY):

- [ ] `00:00–42:13` — dataset, batching, and bigram baseline
- [ ] `42:13–62:00` — weighted aggregation and causal masking
- [ ] `62:00–79:11` — queries, keys, values, and scaled attention
- [ ] `79:11–108:53` — heads, feed-forward layers, residuals, and normalization
- [ ] Use the [timestamped field map](https://idvorkin-ai-tools.github.io/build-gpt-field-map/) when reviewing

## Read the original paper selectively

- [ ] Open [Attention Is All You Need](https://arxiv.org/abs/1706.03762)
- [ ] Read the abstract and introduction
- [ ] Read Section 3: Model Architecture
- [ ] Read Section 5.3: Optimizer
- [ ] Study Figure 1
- [ ] Study Table 1

## Build

- [ ] Implement token embeddings
- [ ] Implement position embeddings
- [ ] Implement one causal self-attention head directly with tensor operations
- [ ] Implement causal masking before softmax
- [ ] Implement scaled dot-product attention
- [ ] Implement multi-head attention
- [ ] Implement the feed-forward network
- [ ] Implement layer normalization
- [ ] Implement residual connections
- [ ] Implement a pre-normalized transformer block
- [ ] Assemble a decoder-only language model

## Tests

- [ ] Future positions receive zero probability
- [ ] Every attention row sums to one
- [ ] Output tensor shapes are correct
- [ ] Batch items never attend to each other
- [ ] Altering future input tokens does not change earlier logits in evaluation mode

## Definition of done

- [ ] I can write the attention equation from memory
- [ ] I can label the shape and purpose of every term
- [ ] I can explain why attention scores are divided by `sqrt(d_k)`
- [ ] I can explain why positional information is necessary
- [ ] I can explain the difference between encoder attention and causal decoder attention

---

# Week 6 — Train and analyze a tiny transformer

## Learn: training stability and systematic debugging

- [ ] Re-read [A Recipe for Training Neural Networks](https://karpathy.github.io/2019/04/25/recipe/)
- [ ] Revisit [Google: Interpreting loss curves](https://developers.google.com/machine-learning/crash-course/overfitting/interpreting-loss-curves)
- [ ] Revisit [PyTorch reproducibility](https://docs.pytorch.org/docs/stable/notes/randomness.html)

## Learn: training configuration and scaling intuition

- [ ] Finish [Karpathy’s GPT lecture](https://www.youtube.com/watch?v=kCc8FmEb1nY)
- [ ] Review [Stanford CS336: Language Modeling from Scratch](https://cs336.stanford.edu/spring2025/) as a deeper reference
- [ ] Watch Lecture 1 in the [CS336 YouTube playlist](https://www.youtube.com/playlist?list=PLoROMvodv4rOY23Y0BoGoBGgQ1zmU_MT_)

## Add experiment tracking

- [ ] Review [W&B experiment tracking](https://docs.wandb.ai/models/ref/python/experiments), or use a local equivalent
- [ ] Record the complete configuration
- [ ] Record parameter count
- [ ] Record train and validation loss
- [ ] Record tokens processed
- [ ] Record wall-clock time
- [ ] Record peak memory
- [ ] Record gradient norm
- [ ] Generate from fixed prompts at regular checkpoints

## Train

- [ ] Choose a small, legally redistributable text corpus
- [ ] Create train and validation splits
- [ ] Confirm the model can overfit a tiny sample
- [ ] Train the full small model
- [ ] Save the best checkpoint
- [ ] Save representative samples from fixed checkpoints

## Controlled experiments

Run at least three experiments while changing one variable at a time:

- [ ] Experiment 1: context length, model size, learning rate, tokenizer, dataset size, or dropout
- [ ] Experiment 2: context length, model size, learning rate, tokenizer, dataset size, or dropout
- [ ] Experiment 3: context length, model size, learning rate, tokenizer, dataset size, or dropout

For each:

- [ ] State the hypothesis
- [ ] State controlled variables
- [ ] Record results
- [ ] Interpret results
- [ ] Document limitations

## Milestone: `tiny-transformer-lab`

- [ ] Clean architecture diagram
- [ ] Source implementation
- [ ] Unit tests
- [ ] Reproducible configuration
- [ ] Learning curves
- [ ] Parameter count and training time
- [ ] Fixed-prompt generations
- [ ] Experiment table
- [ ] Honest failure analysis
- [ ] Public README

---

# Week 7 — Open models, Hugging Face, and baseline evaluation

## Learn: architectures, checkpoints, configurations, and weights

- [ ] Read [Hugging Face: Loading models](https://huggingface.co/docs/transformers/models)
- [ ] Complete [Hugging Face course: Models](https://huggingface.co/learn/llm-course/en/chapter2/3)
- [ ] Bookmark [Transformers documentation](https://huggingface.co/docs/transformers/en/index)
- [ ] Explain architecture versus checkpoint
- [ ] Explain model configuration versus weights
- [ ] Explain `AutoModel` versus `AutoModelForCausalLM`
- [ ] Explain `safetensors` versus pickle-based weight files
- [ ] Explain base versus instruction-tuned checkpoints

## Learn: chat templates

- [ ] Read [Hugging Face: Chat templates](https://huggingface.co/docs/transformers/en/chat_templating)
- [ ] Inspect the exact tokenized form of at least two chat templates
- [ ] Demonstrate one failure caused by incorrect prompt formatting

## Learn: datasets and preprocessing

- [ ] Read [Hugging Face: Processing data](https://huggingface.co/docs/course/main/en/chapter3/2)
- [ ] Read [Datasets: Create a dataset](https://huggingface.co/docs/datasets/en/create_dataset)
- [ ] Read [Datasets: Process](https://huggingface.co/docs/datasets/process)

## Learn: evaluation design

- [ ] Read [HF Evaluation Guidebook: Designing an automatic evaluation](https://github.com/huggingface/evaluation-guidebook/blob/main/contents/automated-benchmarks/designing-your-automatic-evaluation.md)
- [ ] Read [Hugging Face course: Evaluation](https://huggingface.co/docs/course/en/chapter11/5)
- [ ] Read [CS336 evaluation lecture notes](https://cs336.stanford.edu/lectures/?trace=lecture_12)

## Build the baseline before fine-tuning

- [ ] Select a currently supported 0.5B–1.5B model
- [ ] Record the exact model revision
- [ ] Inspect its model card
- [ ] Confirm its license permits the planned work
- [ ] Record parameter count and architecture
- [ ] Inspect tokenizer behavior
- [ ] Inspect chat-template behavior
- [ ] Create a held-out evaluation set
- [ ] Define deterministic metrics where possible
- [ ] Define a failure taxonomy
- [ ] Save raw baseline outputs
- [ ] Save decoding parameters

## Definition of done

- [ ] Evaluation data is separate from training data
- [ ] Model comparisons use the same prompts and decoding settings
- [ ] Results include per-example outputs, not only aggregate scores
- [ ] I can explain why generic benchmarks may not predict target-task performance

---

# Week 8 — Supervised fine-tuning, LoRA, and QLoRA

## Learn: full fine-tuning versus parameter-efficient fine-tuning

- [ ] Read [Hugging Face: LoRA conceptual guide](https://huggingface.co/docs/peft/main/en/conceptual_guides/lora)
- [ ] Read the abstract, introduction, method, and conclusion of the [LoRA paper](https://arxiv.org/abs/2106.09685)
- [ ] Explain `W' = W + BA`
- [ ] Explain why the base weights remain frozen
- [ ] Calculate trainable versus total parameter count

## Learn: rank, alpha, dropout, and target modules

- [ ] Read the relevant fields in [`LoraConfig`](https://huggingface.co/docs/peft/en/package_reference/lora)
- [ ] Read [PEFT configurations and models](https://huggingface.co/docs/peft/guides/peft_model_config)
- [ ] Explain rank `r`
- [ ] Explain `lora_alpha`
- [ ] Explain target-module selection
- [ ] Explain adapter merging and non-merging

## Learn: QLoRA

- [ ] Read the abstract and introduction of the [QLoRA paper](https://arxiv.org/abs/2305.14314)
- [ ] Read the method overview
- [ ] Understand NF4
- [ ] Understand double quantization
- [ ] Understand paged optimizers
- [ ] Complete the relevant [Bitsandbytes quickstart](https://huggingface.co/docs/bitsandbytes/main/en/quickstart)

## Learn: practical supervised fine-tuning

- [ ] Read [TRL `SFTTrainer`](https://huggingface.co/docs/trl/sft_trainer)
- [ ] Work through the [official TRL LoRA/QLoRA Colab](https://github.com/huggingface/trl/blob/main/examples/notebooks/sft_trl_lora_qlora.ipynb)
- [ ] Review the [MLX-LM LoRA/QLoRA guide](https://github.com/ml-explore/mlx-lm/blob/main/mlx_lm/LORA.md) for Apple Silicon

## Prepare data

- [ ] Inspect at least 50 raw examples manually
- [ ] Convert data to the expected conversational or prompt-completion format
- [ ] Inspect tokenized examples
- [ ] Verify special tokens and chat templates
- [ ] Decide whether prompt tokens should be excluded from loss
- [ ] Preserve a validation and test split

## Train and compare

- [ ] Run an untouched baseline
- [ ] Train LoRA or QLoRA configuration A
- [ ] Train configuration B with one controlled change
- [ ] Record trainable parameter count
- [ ] Record peak memory
- [ ] Record training time
- [ ] Record validation loss
- [ ] Evaluate baseline and both adapters identically
- [ ] Check for regressions outside the target task
- [ ] Save qualitative successes and failures

## Definition of done

- [ ] Improvement is measured rather than asserted
- [ ] The baseline remains untouched and reproducible
- [ ] Training data format and loss masking are documented
- [ ] Adapter configuration and base-model revision are saved

---

# Week 9 — Quantization theory and benchmarking

## Learn: quantization fundamentals

- [ ] Read [Hugging Face: Quantization concepts](https://huggingface.co/docs/transformers/quantization/concept_guide)
- [ ] Read [PyTorch: Practical Quantization](https://pytorch.org/blog/quantization-in-practice/)
- [ ] Explain weights versus activations
- [ ] Explain scale and zero-point
- [ ] Explain symmetric versus asymmetric quantization
- [ ] Explain per-tensor versus per-channel quantization
- [ ] Explain calibration
- [ ] Explain post-training quantization versus quantization-aware training

## Learn: choosing a quantization method

- [ ] Read [Hugging Face: Selecting a quantization method](https://huggingface.co/docs/transformers/quantization/selecting)
- [ ] Read [Transformers: Bitsandbytes](https://huggingface.co/docs/transformers/en/quantization/bitsandbytes)
- [ ] Explain why fewer bits do not guarantee lower latency
- [ ] Explain the difference between weight storage and compute precision
- [ ] Explain why hardware kernels determine practical speedups

## Learn: quantization on the M1 Pro

- [ ] Read the relevant [MLX-LM usage](https://github.com/ml-explore/mlx-lm)
- [ ] Read the [`llama.cpp` quantization guide](https://github.com/ggml-org/llama.cpp/blob/master/tools/quantize/README.md)
- [ ] Read the [`llama.cpp` perplexity guide](https://github.com/ggml-org/llama.cpp/blob/HEAD/tools/perplexity/README.md)

## Learn: inference metrics

- [ ] Read [NVIDIA: LLM inference metrics](https://docs.nvidia.com/nim/benchmarking/llm/latest/metrics.html)
- [ ] Define time to first token
- [ ] Define inter-token latency
- [ ] Define prompt-processing throughput
- [ ] Define generation throughput
- [ ] Distinguish throughput from single-request latency

## Benchmark

Compare a supported subset:

- [ ] FP16 or BF16 baseline
- [ ] 8-bit
- [ ] One 5-bit format
- [ ] One 4-bit format
- [ ] Optional: a second 4-bit format

Keep constant:

- [ ] Model and revision
- [ ] Prompts
- [ ] Input lengths
- [ ] Output lengths
- [ ] Warm-up procedure
- [ ] Thread count
- [ ] Generation settings
- [ ] Background machine load as much as practical

Measure:

- [ ] Artifact size
- [ ] Peak process memory
- [ ] Model-load time
- [ ] Time to first token
- [ ] Inter-token latency
- [ ] Prompt tokens per second
- [ ] Generated tokens per second
- [ ] End-to-end latency
- [ ] Task-specific evaluation quality
- [ ] Perplexity where appropriate

## Milestone report

- [ ] Identify the best quality/memory trade-off
- [ ] Identify the best latency configuration
- [ ] State whether lower precision actually increased speed
- [ ] Analyze failure categories that worsened
- [ ] Include raw CSV/JSON measurements
- [ ] Include environment, runtime version, and exact commands

---

# Week 10 — Product-specific evaluation and capstone design

## Learn: task-specific evaluation

- [ ] Read [Hamel Husain: Your AI Product Needs Evals](https://hamel.dev/blog/posts/evals/index.html)
- [ ] Read [OpenAI: Evaluation best practices](https://developers.openai.com/api/docs/guides/evaluation-best-practices)
- [ ] Revisit [HF: Designing an automatic evaluation](https://github.com/huggingface/evaluation-guidebook/blob/main/contents/automated-benchmarks/designing-your-automatic-evaluation.md)
- [ ] Explain why “it looks good” is not an evaluation strategy
- [ ] Explain why application evals differ from general model benchmarks

## Learn: custom evaluation tasks

- [ ] Read [LightEval documentation](https://huggingface.co/docs/lighteval/main/index)
- [ ] Read [LightEval: Adding a custom task](https://huggingface.co/docs/lighteval/en/adding-a-custom-task)
- [ ] Decide whether to use LightEval or a smaller custom harness

## Learn: model documentation and limitations

- [ ] Read [Hugging Face: Model cards](https://huggingface.co/docs/hub/en/model-cards)
- [ ] Review the [annotated model-card template](https://huggingface.co/docs/hub/main/en/model-card-annotated)

## Design the capstone before building it

- [ ] Define the use case
- [ ] Define the target user
- [ ] Define typed input/output behavior
- [ ] Define measurable success criteria
- [ ] Create 50–100 initial evaluation cases
- [ ] Select and measure a baseline
- [ ] Define failure categories
- [ ] Draw the architecture
- [ ] Define latency and memory budgets
- [ ] Define out-of-scope behavior
- [ ] Record privacy considerations
- [ ] Record safety and misuse considerations

## Definition of done

- [ ] Another engineer could use the specification to compare two system versions
- [ ] Evaluation examples represent the actual target task
- [ ] Expected behavior and scoring are explicit
- [ ] The design is narrow enough to finish in two weeks

---

# Week 11 — Serving, streaming, performance, and observability

## Learn: model-as-a-service architecture

- [ ] Review [Full Stack Deep Learning: Deployment and monitoring](https://fullstackdeeplearning.com/spring2021/lecture-11/)
- [ ] Watch the [deployment lecture](https://www.youtube.com/watch?v=jFflwpx4iK0)
- [ ] Explain model-in-service versus model-as-a-service

## Learn: typed APIs and error handling

- [ ] Use the [FastAPI tutorial](https://fastapi.tiangolo.com/tutorial/) for request models, response models, lifecycle, and testing
- [ ] Read [FastAPI: Error handling](https://fastapi.tiangolo.com/tutorial/handling-errors/)

## Learn: token streaming

- [ ] Read [Hugging Face: Generation streaming](https://huggingface.co/docs/transformers/en/generation_features)
- [ ] Read [FastAPI: Streaming data](https://fastapi.tiangolo.com/advanced/stream-data/)

## Learn: batching, KV caching, prefix caching, and serving

- [ ] Read the [vLLM overview](https://docs.vllm.ai/)
- [ ] Read [Inside vLLM: Anatomy of a high-throughput inference system](https://vllm.ai/blog/2025-09-05-anatomy-of-vllm)
- [ ] Explain prefill versus decode
- [ ] Explain KV caching
- [ ] Explain continuous batching
- [ ] Explain prefix caching
- [ ] Explain why these features change latency/throughput trade-offs

## Build the service

- [ ] Add typed inference request and response schemas
- [ ] Add a health endpoint
- [ ] Load the model once during application startup
- [ ] Add non-streaming inference
- [ ] Add streaming inference
- [ ] Add input-length limits
- [ ] Add request timeouts
- [ ] Add structured error responses
- [ ] Add request IDs
- [ ] Log model version
- [ ] Log generation configuration
- [ ] Log input/output token counts
- [ ] Log latency metrics
- [ ] Write API tests using a mocked model
- [ ] Write at least one integration test using the real model

## Benchmark the service

Use [NVIDIA’s inference metric definitions](https://docs.nvidia.com/nim/benchmarking/llm/latest/metrics.html):

- [ ] Measure p50 latency
- [ ] Measure p95 latency
- [ ] Measure time to first token
- [ ] Measure generated tokens per second
- [ ] Record prompt and output lengths
- [ ] Record peak memory
- [ ] Record errors and timeouts

## Definition of done

- [ ] Service behavior is testable without loading the real model
- [ ] The real model is tested through the service boundary
- [ ] Streaming improves perceived latency
- [ ] Performance numbers include methodology and workload details

---

# Week 12 — Final evaluation, release, and public explanation

## Run final comparisons

Evaluate with the fixed Week 10 suite:

- [ ] Original baseline model
- [ ] Fine-tuned model
- [ ] Chosen quantized model
- [ ] Deployed service
- [ ] Preserve parsing and generation failures in the results
- [ ] Save raw per-example outputs
- [ ] Produce aggregate metrics by failure category

## Write model and project documentation

- [ ] Revisit [Hugging Face: Model cards](https://huggingface.co/docs/hub/en/model-cards)
- [ ] Use the [annotated model-card template](https://huggingface.co/docs/hub/main/en/model-card-annotated)
- [ ] Document intended use
- [ ] Document architecture and base model
- [ ] Document dataset provenance and license
- [ ] Document training settings
- [ ] Document hardware and runtime
- [ ] Document evaluation methodology
- [ ] Include benchmark tables
- [ ] Include latency and memory results
- [ ] Document limitations and known failures
- [ ] Include exact reproduction instructions

## Write the technical article

- [ ] Problem and hypothesis
- [ ] Baseline
- [ ] Dataset and evaluation methodology
- [ ] Fine-tuning method
- [ ] Quantization method
- [ ] Results
- [ ] Unexpected findings
- [ ] Failure analysis
- [ ] Deployment architecture
- [ ] Reproduction instructions

## Package the portfolio

- [ ] Clean GitHub repository
- [ ] Concise README
- [ ] Architecture diagram
- [ ] Evaluation report
- [ ] Model card
- [ ] Benchmark data in CSV or JSON
- [ ] Short demonstration video
- [ ] Deployed or locally reproducible demo
- [ ] One long technical article
- [ ] Three to five short posts derived from real findings
- [ ] Résumé bullets using measured outcomes

## Final acceptance criteria

A hiring engineer can determine:

- [ ] What I implemented personally
- [ ] What came from libraries
- [ ] How the system was evaluated
- [ ] Whether fine-tuning improved the target behavior
- [ ] What quantization changed
- [ ] What trade-offs and failures I discovered
- [ ] How to reproduce the work

---

# Publishing tracker

Avoid daily “learning in public” filler. Publish when there is an actual observation, implementation, or result.

## Short technical posts

- [ ] Week 1: Learning-rate experiment and loss curves
- [ ] Week 2: Visual explanation of backpropagation through one graph
- [ ] Week 3: Why overfitting one batch is a useful debugging test
- [ ] Week 4: Character versus subword tokenization comparison
- [ ] Week 5: Attention tensor shapes and causal masking
- [ ] Week 6: Tiny-transformer experiment result
- [ ] Week 7: A chat-template or evaluation failure you discovered
- [ ] Week 8: LoRA configuration comparison
- [ ] Week 9: Quantization benchmark result
- [ ] Week 10: How the capstone evaluation set was designed
- [ ] Week 11: Latency/throughput findings
- [ ] Week 12: Final capstone results

## Substantial write-ups

- [ ] Phase 1: From gradient descent to an autograd engine
- [ ] Phase 2: Building and training a tiny transformer
- [ ] Phase 3: Fine-tuning and quantization study
- [ ] Phase 4: Production-style capstone

---

# Weekly review template

Copy this section into the learning log at the end of each week.

```markdown
## Week N review

### Completed
- 

### What I can now explain without notes
- 

### Experiments run
| Experiment | Hypothesis | Result | Interpretation |
|---|---|---|---|
| | | | |

### Bugs or failed attempts
- 

### Questions still open
- 

### Artifact produced
- Repository/commit:
- Report/post:

### Next week’s carry-over
- 
```

---

# Experiment record template

```markdown
## Experiment: <name>

- Date:
- Git commit:
- Model and revision:
- Dataset and revision:
- Hardware:
- Software versions:
- Seed:

### Hypothesis

### Configuration

### Controlled variables

### Metrics

### Results

### Failure examples

### Interpretation

### Limitations

### Next experiment
```

---

# Deferred topics

Do not add these to the core 12-week schedule:

- [ ] Complete Andrew Ng specialization
- [ ] Distributed multi-node pretraining
- [ ] Custom CUDA kernels
- [ ] RLHF, PPO, DPO, or GRPO
- [ ] Mixture-of-experts training
- [ ] Multimodal models
- [ ] Advanced scaling-law research
- [ ] Training a billion-parameter model from scratch

Revisit them only after completing the core roadmap.

---

# Core resource index

- [Karpathy: Neural Networks Zero to Hero](https://karpathy.ai/zero-to-hero.html)
- [PyTorch beginner tutorials](https://docs.pytorch.org/tutorials/beginner/basics/intro.html)
- [Hugging Face LLM course](https://huggingface.co/learn/llm-course/)
- [Stanford CS336: Language Modeling from Scratch](https://cs336.stanford.edu/spring2025/)
- [MLX-LM](https://github.com/ml-explore/mlx-lm)
- [`llama.cpp`](https://github.com/ggml-org/llama.cpp)
- [Hugging Face PEFT](https://huggingface.co/docs/peft/)
- [Hugging Face TRL](https://huggingface.co/docs/trl/)
- [Hugging Face LightEval](https://huggingface.co/docs/lighteval/main/index)
