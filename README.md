# 23619007

# Paper Review: Text-Conditioned Diffusion Model for High-Fidelity Korean Font Generation

**Authors**: Abdul Sami, Avinash Kumar, Irfanullah Memon, Youngwon Jo, Muhammad Rizwan, Jaeyong Choi  
**Affiliation**: Soongsil University  
**arXiv**: [2504.21325](https://arxiv.org/abs/2504.21325)  
**Year**: 2024

## 1. Research Background and Purpose

This paper proposes a high-fidelity automatic Korean font generation method named **DK-Font**, which utilizes a text-conditioned diffusion model. Existing GAN/VAE-based methods often suffer from training instability, mode collapse, and difficulty preserving fine stylistic details, especially in complex languages like Korean. The proposed approach aims to solve these limitations by integrating phonetic character encoding and a robust diffusion framework.

## 2. Method Overview

### Dataset

- Korean font dataset with 210 styles (105 handwritten, 105 printed)
- Each font contains 2,350 commonly used Korean characters
- Split: 200 fonts for training, 10 for testing (5 per category)

### Preprocessing

- Image size normalized to 128×128 pixels
- Character-level phonetic information (Choseong, Jungseong, Jongseong) embedded as text input vectors

### Model Architecture

- **Backbone**: U-Net-based Diffusion Model
- **Text Encoder**: Encodes phonetic features of characters
- **Style Encoder**: DG-Font pretrained encoder used
- **Character Attributes Encoder**: Integrates text, stroke, and style information into a latent representation `z`
- **Loss Function**:
  - Perceptual Loss using VGG-19
  - Mean Squared Error (MSE)

### Training Settings

- Optimizer: AdamW
- Learning Rate: 0.001
- Batch Size: 16
- Iterations: 50,000
- Noise Scheduler: cosine
- Dropout: 0.1

## 3. Experimental Results

### Evaluation Metrics

- **SSIM (↑)**: Structural Similarity Index
- **RMSE (↓)**: Root Mean Square Error
- **LPIPS (↓)**: Learned Perceptual Image Patch Similarity
- **FID (↓)**: Fréchet Inception Distance

### Quantitative Comparison

| Model     | SSIM | RMSE  | LPIPS | FID    |
|-----------|------|-------|--------|--------|
| Diff-Font | 0.812 | 0.196 | 0.072 | 10.690 |
| DK-Font   | 0.857 | 0.123 | 0.063 | 10.446 |

- DK-Font outperforms Diff-Font in all metrics
- Visual comparison also shows more structurally consistent and stylistically coherent results in both handwritten and printed font styles

## 4. Limitations

- The method is tested only on Korean character datasets; generalization to other scripts (e.g., Latin, Chinese) is not verified
- May be sensitive to input image quality, especially in one-shot settings
- Further experiments are needed on irregular and ambiguous character forms

## 5. Summary

The paper introduces **DK-Font**, a text-conditioned diffusion model capable of generating full sets of high-quality Korean fonts using only a single reference character.  
By integrating phonetic text encodings and perceptual loss, the model achieves superior visual and structural accuracy compared to previous methods.  
This approach demonstrates the potential of adapting vision-language models like SAM and Diffusion for complex character-based languages.
