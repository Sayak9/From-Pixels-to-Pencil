# From Pixels to Pencil: Exploring Image Sketching with OpenCV

What does it take to turn an ordinary photograph into something that resembles a pencil drawing? This project explores how a series of simple image processing techniques can transform a colour image into a monochromatic sketch.

Using Python and OpenCV, I experiment with grayscale conversion, image inversion, Gaussian blurring and dodge blending to recreate the appearance of a pencil sketch. I also compare different blur strengths and explore an optional contrast enhancement technique to see how they affect the final result.

The idea is to understand how each transformation contributes to the overall effect, rather than simply applying a predefined image filter.

## Project Overview

The objective is to take a colour photograph and progressively transform it into a pencil sketch using OpenCV.

The process involves working with pixel intensity values, manipulating contrast and blending different versions of the same image.

The notebook also explores how changing the Gaussian blur kernel influences the final appearance and whether local contrast enhancement can bring out additional details.

## Tools and Technologies

1. **Python:** Image processing and overall implementation.
2. **OpenCV:** Image loading, colour conversion, inversion, Gaussian blur and pixelwise blending.
3. **NumPy:** Working with image arrays and pixel values.
4. **Matplotlib:** Displaying the original image, intermediate transformations and final results.
5. **Jupyter Notebook:** Organising the experiment and documenting each stage.

## Methodology

### 1. Loading the Image

The first step is to load a colour photograph using OpenCV.

Since OpenCV reads images in BGR channel order by default, the image is converted into RGB format before applying the remaining transformations.

The notebook supports both local image loading and direct image uploads through Google Colab.

### 2. Grayscale Conversion

The colour image is converted into grayscale, reducing each pixel to a single intensity value.

This removes colour information while retaining the light and dark regions that will eventually form the pencil sketch.

### 3. Image Inversion

The grayscale image is inverted to create its negative.

Dark regions become bright, while bright regions become dark. This inverted image acts as the starting point for the next transformation.

### 4. Gaussian Blur

A Gaussian blur is applied to the inverted image to soften its details and create smoother tonal transitions.

The blur strength is controlled through the kernel size. The initial experiment uses a kernel of 21 by 21 pixels.

### 5. Dodge Blending

The blurred image is inverted once again and combined with the original grayscale image through pixelwise division.

This technique, commonly known as dodge blending, brightens smoother regions while retaining darker outlines and details.

The operation is performed using OpenCV's `cv2.divide()` function with a scale factor of 256.

The resulting image produces the characteristic pencil sketch effect.

### 6. Experimenting with Blur Strength

Different photographs can respond differently to the same processing settings.

To explore this, the notebook compares three Gaussian blur kernel sizes:

1. 11 by 11 pixels.
2. 21 by 21 pixels.
3. 31 by 31 pixels.

The comparison helps illustrate how blur strength affects the balance between fine details, outlines and softer shading.

### 7. Improving Contrast with CLAHE

As an additional experiment, I use Contrast Limited Adaptive Histogram Equalization, commonly known as CLAHE.

It enhances local contrast in the grayscale image before repeating the sketch generation process.

This provides an alternative result that can help bring out details in photographs where the basic pencil sketch effect appears somewhat flat.

The enhanced version is compared with the original result to see whether the additional contrast produces a more convincing sketch.

## Output

The notebook generates two versions of the processed image:

| Output file | Description |
|---|---|
| `pencil_sketch.png` | Standard pencil sketch using Gaussian blur and dodge blending |
| `pencil_sketch_enhanced.png` | Sketch generated using CLAHE enhanced grayscale input |

Both images are saved automatically in an `output` directory.

## How to Run the Project

The notebook can be executed locally using Jupyter Notebook or through Google Colab.

### 1. Install the required libraries

```bash
pip install opencv-python numpy matplotlib
```

### 2. Provide an input image

For local execution, place a colour JPG or PNG image in the same directory as the notebook and name it `input_image.jpg`.

Alternatively, change the `IMAGE_PATH` variable in the notebook to match your image filename.

When using Google Colab, the notebook provides an upload option, so there is no need to configure a local file path.

### 3. Execute the notebook

Run the cells sequentially to follow the image processing workflow, compare intermediate transformations and experiment with different blur settings.

### 4. Retrieve the results

The generated pencil sketches will be available inside the `output` directory.

## Conclusion

This experiment demonstrates how a relatively simple sequence of image processing operations can produce an interesting artistic transformation.

One of the most interesting aspects was seeing how much the final result changes with different Gaussian blur settings. The optional CLAHE enhancement also provides another way to experiment with contrast and image detail.

Rather than relying on a ready made filter, the project builds the sketch effect step by step, making it easier to understand how individual pixel transformations contribute to the final image.
