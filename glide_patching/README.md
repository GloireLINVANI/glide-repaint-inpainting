# GLIDE Patching

Contains the code of the method. With the `glide-text2im` library installed, it loads GLIDE's models and patches their sampling to use RePaint's resampling schedule.

* `prepare_glide_inpaint.py`: Creates GLIDE's 64×64 model or its 256×256 upsampler, in the base or the inpainting version, and loads the released checkpoint.
* `repaint_patcher.py`: RePaint's jump schedule and sampling loop, adapted from the [RePaint repository](https://github.com/andreas128/RePaint), and `patch_model_for_repaint`, which makes a GLIDE diffusion object sample with them. Like RePaint's code, this file is under [CC BY-NC-SA 4.0](https://creativecommons.org/licenses/by-nc-sa/4.0/).
* `repaint_sampling.py`: Two samplers for each of the three variants (GLIDE-Inpaint, GLIDE-Base w/ RePaint, and GLIDE-Inpaint w/ RePaint): one for the 64×64 model, which applies classifier-free guidance, and one for the upsampler.
* `image_util.py`: Helpers to load, generate, convert, display, and save images and masks.
