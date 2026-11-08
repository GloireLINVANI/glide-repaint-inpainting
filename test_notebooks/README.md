# Test Notebooks

Contains the notebooks used for testing and development, kept for reference. They date from before the code moved to `glide_patching/` and were not updated: they import its modules as if they sat next to them, use paths relative to the repository root, and read files that are not in this repository, such as the datasets and RePaint's example face image and mask. Expect to adapt them before running them.

## Notebooks
* `batch_process_masks.ipynb`: Notebook that the evaluation script `process_datasets.py` was based on.
* `inpaint_face_repaint.ipynb`: First test patching the GLIDE model with the RePaint sampling strategy. It uses the face image provided with RePaint, but the notebook is loosely based on the one provided with GLIDE.
* `inpaint_face.ipynb`: Test trying the GLIDE inpainting model on the inpainting task from the RePaint paper (with a literal mask). It fails catastrophically due to OpenAI's filtering; see the GLIDE paper's appendix on safety.
* `sample_coco_for_human_eval.ipynb`: The notebook used to generate the images for the human evaluation survey.
* `test_repaint.ipynb`: Applies the RePaint patching to batches of images based on the grass image provided with GLIDE, and compares the models to determine comparable parameters for each.
* `upscale_images.ipynb`: Notebook used as the basis of `upscale_simple.py` and `upscale_full.py`. It also contains the code that randomly selected which of the generated 64×64 images to upscale.
