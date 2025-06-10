## Best-of-the-Best Local AI Models for 4GB GPUs

**Warning:** Using AI models on a 4GB GPU is a significant challenge. This VRAM tier is extremely constrained, and models will push the limits of what's possible. Expect:
* **Aggressive Quantization:** Almost all models will require `Q2_K` or `Q3_K_M` quantization, leading to noticeable quality degradation.
* **Frequent CPU Offloading:** Performance will often be bottlenecked by CPU RAM and bus speed, resulting in very slow inference.
* **Severe Limitations:** Context windows for LLMs will be very short, and image/video generation will be limited to extremely low resolutions and short durations, with visible artifacts.
* **Trailblazer Mentality:** Few users operate at this VRAM level for advanced AI tasks, so community support for specific issues you encounter may be limited. Expect to spend significant time troubleshooting and experimenting.

**Legend:**
* `⭐`: **MUST-HAVE.** Essential for most users, offering foundational capabilities or exceptional general utility despite limitations.
* `✨`: **HIGHLY RECOMMENDED / SPECIALIZED ALTERNATIVE.** Excellent alternatives or crucial for specific niche use cases, often with significant caveats.

---

### Large Language Models (General Purpose Text Generation)

| Model Name | Recommended Variant/Quantization (for 4GB VRAM) | Ideal Usage Scenario | Comments |
|:--------------------------|:------------------------------------------------|:----------------------------------------------------|:------------------------------------------------------------------------------------------------------------------------------------------------------|
| **Phi-3-Mini** ⭐ | `3.8B` (**Q4_K_M** or **Q3_K_M**) | Rapid prototyping, quick answers, basic text generation | ⭐ An incredibly efficient model, often providing nearly instant responses for straightforward text tasks. It represents the fastest and most reliable general-purpose LLM on 4GB GPUs. |
| **Mistral 7B Instruct** ✨ | `7B` (**Q3_K_M** or **Q2_K**) | General chat, summarization (short texts), basic reasoning | ✨ A highly efficient and capable model, even at low bitrates. The `Q3_K_M` or `Q2_K` variant is the largest truly usable 7B-class model, offering a balance of capability and extreme VRAM efficiency, though with **noticeable quality degradation and slow inference speeds**. |

---

### Large Language Models (Coding-Specific Text Generation)

| Model Name | Recommended Variant/Quantization (for 4GB VRAM) | Ideal Usage Scenario | Comments |
|:-----------------------------------|:------------------------------------------------|:----------------------------------------------------|:------------------------------------------------------------------------------------------------------------------------------------------------------|
| **Phi-3-Mini** ⭐ | `3.8B` (**Q4_K_M** or **Q3_K_M**) | Autocompletion, simple function generation, syntax lookup | ⭐ Its extreme compactness and speed make it indispensable for quick, iterative coding tasks and basic code assistance, providing immediate value on 4GB GPUs. |
| **DeepSeek-Coder 7B Instruct** ✨ | `7B` (**Q3_K_M** or **Q2_K**) | General programming (simple), code generation (short snippets) | ✨ Renowned for its coding performance. The `Q3_K_M` or `Q2_K` variant is the most ambitious coding model for 4GB, but expect **significant quality compromise and very slow inference**, especially for complex or longer code. |

---

### Image Analysis Models (Visual Understanding, Captioning, Tagging)

| Model Name | Recommended Variant/Quantization (for 4GB VRAM) | Ideal Usage Scenario | Comments |
|:---------------------------------|:------------------------------------------------|:----------------------------------------------------|:------------------------------------------------------------------------------------------------------------------------------------------------------|
| **CLIP (e.g., OpenAI ViT-B/32)** ⭐ | `ViT-B/32` (**fp16** or **Q8**) | Zero-shot image classification, image similarity search (basic), text-to-image relevance | ⭐ A foundational model for understanding text-image relationships. The smaller `ViT-B/32` variant runs efficiently at `fp16` or `Q8`, offering highly versatile image analysis capabilities within 4GB. |
| **DeepBooru** ⭐ | (Standard release, typically `fp16` or optimized) | Automatic anime-style image tagging, dataset creation for anime models | ⭐ An efficient model specialized in generating tags for anime/manga content. It runs very fast on 4GB GPUs, making it a valuable and practical tool for this specific niche. |
| **BLIP / BLIP-2 (e.g., BLIP Base)** ✨ | `Base` (**Q4_K_M** or `Q3_K_M`) | Image captioning (short), basic visual question answering | ✨ An excellent model for generating descriptive captions. On 4GB GPUs, it will likely require aggressive quantization, leading to **slower performance and potentially less nuanced captions**. |

---

### Generative Image Models

**Severe Caveats for 4GB GPUs:** Generating *any* usable images on 4GB VRAM is extremely challenging. Expect:
* **Low Resolution:** Likely limited to `512x512` and even that will be slow and memory-intensive. Higher resolutions are generally not feasible.
* **Low Quality:** Significant visual artifacts (e.g., blurriness, distortions) due to aggressive quantization and limited VRAM.
* **Very Slow:** Generation will be slow, often measured in minutes per image.
* **Limited Workflows:** Complex features like ControlNet or multiple LoRAs are generally not supported.

| Model Name | Recommended Variant/Quantization (for 4GB VRAM) | Ideal Usage Scenario | Comments |
|:-------------------------------|:------------------------------------------------|:---------------------------------------------------------|:------------------------------------------------------------------------------------------------------------------------------------------------------|
| **Stable Diffusion 1.5 (SD 1.5)** ✨ | `Base` (**Q4_K_M** or **Q3_K_M**, with **LCM LoRA**) | Basic image generation (512x512), artistic concepts (low fidelity) | ✨ SD 1.5 is the only broadly viable generative image model on 4GB. It requires aggressive quantization (e.g., `Q3_K_M`) combined with **optimized LoRAs like LCM** for any practical speed. Expect **significant visual artifacts and slow generation** at `512x512`. |
| **FLUX.1 Schnell** ✨ | `Schnell FP8` (if available and highly optimized) | Experimental fast image generation (extremely limited) | ✨ Optimized for speed and lower VRAM usage. If a highly optimized `FP8` variant exists, it might offer experimental fast image generation, but will still face severe resolution and quality limitations on 4GB VRAM. |

---

### Generative Video Models

**Extremely Challenging for 4GB GPUs:** Video generation is largely impractical on 4GB VRAM. If it runs at all, it will be:
* **Tiny Resolutions:** Often `256x256` or lower.
* **Very Short Clips:** A few seconds at most.
* **Severe Artifacts:** High levels of quality degradation and visual glitches.
* **Astronomical Generation Times:** Minutes per second of video.

| Model Name | Recommended Variant/Quantization (for 4GB VRAM) | Ideal Usage Scenario | Comments |
|:-----------------------------|:------------------------------------------------|:-----------------------------------------------|:------------------------------------------------------------------------------------------------------------------------------------------------------|
| (No practical recommendations for consistent performance or quality) | | | Attempting generative video on 4GB VRAM is typically not feasible for usable output. The memory constraints are too severe for consistent performance, requiring pioneering efforts and extreme patience for minimal results. |

---

### Generative Audio Models

| Model Name | Recommended Variant/Quantization (for 4GB VRAM) | Ideal Usage Scenario | Comments |
|:---------------------------------|:------------------------------------------------|:---------------------------------------------------|:------------------------------------------------------------------------------------------------------------------------|
| **Whisper.cpp** ⭐ | `small.en` or `medium.en` (Optimized/Quantized) | Speech-to-Text, Transcription | ⭐ A **MUST-HAVE** for speech-to-text. It runs incredibly efficiently on 4GB GPUs, enabling very fast and accurate transcriptions, even for its smaller variants. |
| **MAGNET (Meta)** ✨ | (Standard local release, highly optimized) | Basic music/audio synthesis from text/prompts | ✨ A capable model for music generation. Highly optimized local releases might be runnable on 4GB GPUs for basic synthesis, but larger or more complex outputs could hit VRAM limits. |
