# Text-Conditioned Diffusion Inpainting with RePaint Sampling

Course project for *Multimodal Generative AI* (MSc Data and AI, École Polytechnique), by Gloire Linvani and Kenneth Browder.

[GLIDE](https://github.com/openai/glide-text2im) is OpenAI's text-to-image diffusion model, released with a version fine-tuned for inpainting. [RePaint](https://github.com/andreas128/RePaint) inpaints with a diffusion model that was never trained for inpainting: at every step, it replaces the known part of the image with a noised copy of the original, and it repeatedly adds noise back and denoises again (resampling) so that the generated region blends in with the rest. This project brings RePaint's sampling to GLIDE while keeping its text guidance (classifier-free guidance) at every step, and compares three variants: GLIDE's inpainting model (GLIDE-Inpaint), GLIDE's base model with RePaint sampling (GLIDE-Base w/ RePaint), and GLIDE-Inpaint with RePaint sampling (GLIDE-Inpaint w/ RePaint). The evaluation covers MS-COCO, ImageNet, and Places365 images with six mask types, and uses FID, LPIPS, and a blind human evaluation.

> **Version note.** The version submitted for grading in March 2025 is tagged [`submitted`](https://github.com/GloireLINVANI/glide-repaint-inpainting/tree/submitted). Since then, the repository has been renamed from `CSC_52002_EP_Generative_AI_Project`, the READMEs have been revised, the report has been added, and the papers' PDFs and the RePaint submodule have been replaced with links. The code is unchanged.

## Contents

| Path | Description |
|---|---|
| `report.pdf` | Report: method, evaluation protocol, results, and sample images |
| `Inpainting_GLIDE_and_RePaint.ipynb` | Demo: a Gradio app that inpaints your own images with the three variants |
| `glide_patching/` | The method: loads GLIDE, patches RePaint's resampling into its sampling, and defines the three variants' samplers |
| `eval_scripts/` | Scripts that generated, upsampled, and scored the evaluation images |
| `data/` | Masks, example images, dataset download scripts, and the FID and LPIPS scores |
| `report_evaluation_data.xlsx` | The report's tables, computed from the CSV files in `data/eval_csv/` |
| `test_notebooks/` | Development notebooks, kept for reference |
| `glide-text2im/` | GLIDE's repository, as a submodule at the version used |

## Running the demo

The demo is written for Google Colab, ideally with a GPU.

1. Open [`Inpainting_GLIDE_and_RePaint.ipynb` in Colab](https://colab.research.google.com/github/GloireLINVANI/glide-repaint-inpainting/blob/main/Inpainting_GLIDE_and_RePaint.ipynb).
2. Run all cells. The notebook installs the dependencies, clones this repository, downloads the GLIDE checkpoints, and opens a Gradio app: upload an image, paint over the region to fill, and enter a prompt.

## Reproducing the evaluation

The demo is all you need to try the method. The scripts in `eval_scripts/` generated, upsampled, and scored the evaluation images, and their README describes what each one reads and writes. `data/README.md` explains how to get the datasets.

The `glide-text2im` submodule pins the version of GLIDE used: `git submodule update --init` fetches it, and `pip install ./glide-text2im` installs it.

## References

- J. Ho, A. Jain, and P. Abbeel. *Denoising Diffusion Probabilistic Models.* NeurIPS 2020. [arXiv:2006.11239](https://arxiv.org/abs/2006.11239)
- A. Nichol, P. Dhariwal, A. Ramesh, P. Shyam, P. Mishkin, B. McGrew, I. Sutskever, and M. Chen. *GLIDE: Towards Photorealistic Image Generation and Editing with Text-Guided Diffusion Models.* ICML 2022. [arXiv:2112.10741](https://arxiv.org/abs/2112.10741)
- A. Lugmayr, M. Danelljan, A. Romero, F. Yu, R. Timofte, and L. Van Gool. *RePaint: Inpainting using Denoising Diffusion Probabilistic Models.* CVPR 2022. [arXiv:2201.09865](https://arxiv.org/abs/2201.09865)

## Credits and license

GLIDE's code and checkpoints come from OpenAI's [glide-text2im](https://github.com/openai/glide-text2im) repository (MIT License), and the samplers in `glide_patching/repaint_sampling.py` build on its example notebooks. `glide_patching/repaint_patcher.py` adapts code from the [RePaint](https://github.com/andreas128/RePaint) repository (Huawei Technologies, CC BY-NC-SA 4.0), so that file is distributed under the same license, [CC BY-NC-SA 4.0](https://creativecommons.org/licenses/by-nc-sa/4.0/).
