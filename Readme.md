-----

# SlideLab: A Modular Framework for WSI Preprocessing

\<p align="center"\>
\<img src="https/[github.com/user-attachments/assets/1e89103a-e79b-484d-818f-17cfa828380d](https://github.com/user-attachments/assets/1e89103a-e79b-484d-818f-17cfa828380d)" alt="SlideLab Workflow" width="800"/\>
\</p\>
\<p align="center"\>
\<strong\>Lorenzo Olmo Marchal\</strong\>\<br\>
M.S. Thesis, University of California San Diego, 2025\<br\>
\<a href="[https://www.linkedin.com/in/lorenzo-olmo-marchal-b80508271/](https://www.linkedin.com/in/lorenzo-olmo-marchal-b80508271/)" target="\_blank"\>LinkedIn\</a\> | Advisor: \<a href="[https://profiles.ucsd.edu/ludmil.alexandrov](https://profiles.ucsd.edu/ludmil.alexandrov)" target="\_blank"\>Prof. Ludmil B. Alexandrov\</a\> | \<a href="[https://alexandrov.cloud.ucsd.edu/home](https://alexandrov.cloud.ucsd.edu/home)" target="\_blank"\>Alexandrov Lab\</a\>
\</p\>

## Table of Contents

  - [Abstract](https://www.google.com/search?q=%23abstract)
  - [Project Highlights](https://www.google.com/search?q=%23project-highlights)
  - [Presentation](https://www.google.com/search?q=%23presentation)
  - [Installation](https://www.google.com/search?q=%23installation)
  - [Usage](https://www.google.com/search?q=%23usage)
  - [Arguments](https://www.google.com/search?q=%23arguments)
  - [License](https://www.google.com/search?q=%23license)
  - [Contact](https://www.google.com/search?q=%23contact)
  - [References](https://www.google.com/search?q=%23references)

## Abstract

Computational pathology has emerged as a rapidly advancing subspecialty focused on the quantitative, large-scale analysis of pathological data like Whole Slide Images (WSIs). This work addresses significant challenges in preprocessing and model interpretability within this field. The core contributions are twofold: first, the development of SlideLab, a novel and robust preprocessing module designed to optimize the creation of high-quality WSI datasets; second, the introduction of a new interpretability method, Polarized Attentional Confidence (PAC), to enhance the transparency and trustworthiness of AI systems in pathology.

## Project Highlights

### Project Analysis 🧠

This thesis effectively tackles two of the most significant hurdles in computational pathology: the lack of standardized preprocessing and the interpretability of "black box" AI models. The project is logically divided into two main contributions:

  * **SlideLab (The Preprocessing Framework):** A modular and comprehensive solution to the rigid and irreproducible nature of existing tools. It addresses key WSI challenges like computational cost, stain variability, and artifacts through a sophisticated, GPU-accelerated architecture.
  * **Polarized Attentional Confidence (PAC) (The Interpretability Method):** An intelligent approach to address clinical trust in AI. By combining a model's attention (importance) and probability (confidence), PAC creates a robust metric to validate that models are learning biologically relevant features.

### Key Achievements 🏆

  * **Development of a Novel and Complete Tool:** Built a functional, end-to-end software pipeline, SlideLab.
  * **Superior Performance Through Benchmarking:** Rigorously tested SlideLab against five other state-of-the-art pipelines, achieving the highest Dice score (0.741) for tissue segmentation.
  * **Improved Downstream Model Performance:** Demonstrated that better preprocessing leads to better science, as the model trained on SlideLab-processed data outperformed others.
  * **Innovation in Model Interpretability:** Proposed PAC as a new method tailored to the specific challenges of multi-instance learning in pathology.
  * **Validation with Real-World Case Studies:** Successfully applied PAC to clinically relevant problems in colorectal cancer and leukemia.

### Summary of Results 📊

  * **SlideLab is Quantifiably Better:** The framework produces higher-quality data, evidenced by superior Dice scores and improved downstream model performance.
  * **PAC Provides Deeper Biological Insight:** Case studies in MSI and B-ALL demonstrated that PAC can validate a model's reasoning by correctly identifying biologically and clinically relevant features.

\<p align="center"\>
\<img src="[https://i.imgur.com/Z4xYf7o.png](https://i.imgur.com/Z4xYf7o.png)" alt="Benchmarking Results" width="700"/\>
\</p\>

## Presentation

\<p align="center"\>
\<iframe src="[https://docs.google.com/presentation/d/e/2PACX-1vTcRNQw8tuWOTNT9N4M-BG6-BgthZ8xFAdRBFbIXvUXN-DbKEyDU3ky53QZp3wOFqZVElVexLXJ-Lap/pubembed?start=false\&loop=false\&delayms=3000](https://docs.google.com/presentation/d/e/2PACX-1vTcRNQw8tuWOTNT9N4M-BG6-BgthZ8xFAdRBFbIXvUXN-DbKEyDU3ky53QZp3wOFqZVElVexLXJ-Lap/pubembed?start=false&loop=false&delayms=3000)" frameborder="0" width="960" height="569" allowfullscreen="true" mozallowfullscreen="true" webkitallowfullscreen="true"\>\</iframe\>
\</p\>

## Installation

First, clone the repository and navigate into the project directory:

```bash
git clone https://github.com/lolmomarchal/SlideLab.git
cd SlideLab
```

To install the required dependencies, create and activate the Conda environment using the provided file:

```bash
conda env create -f environment.yml
conda activate slidelab
```

## Usage

Below is an example command to run the full preprocessing pipeline on a directory of slides:

```bash
python SlidePreprocessing.py -i /path/to/input/ -o /path/to/output/ \
  -s 512 -m 40 --remove_blurry_tiles --normalize_staining --encode \
  -th 0.8 -bh 0.02 --device cuda --batch_size 256
```

## Arguments

The pipeline's behavior can be customized with various arguments. Here are some of the most common ones:

| Argument                        | Description                                      | Default       |
| :------------------------------ | :----------------------------------------------- | :------------ |
| `-i`, `--input_path`            | Path to the input WSI file(s)                    | **Required**  |
| `-o`, `--output_path`           | Path to save the output tiles                    | **Required**  |
| `-s`, `--desired_size`          | Desired size of tiles in pixels                  | `256`         |
| `-m`, `--desired_magnification` | Desired magnification level (e.g., 20x)          | `20`          |
| `-ov`, `--overlap`              | Factor of overlap between tiles (1 = no overlap) | `1`           |
| `-rb`, `--remove_blurry_tiles`  | Remove blurry tiles using a Laplacian filter     | `False`       |
| `-n`, `--normalize_staining`    | Normalize the staining of the tiles              | `False`       |
| `-e`, `--encode`                | Encode tiles into a `.h5` file for deep learning | `False`       |
| `-th`, `--tissue_threshold`     | Minimum tissue content to consider a tile valid  | `0.7`         |
| `--device`                      | Specify device for computation (e.g., cuda, cpu) | `Auto-detect` |

## License

This project is licensed under the MIT License.

> Copyright (c) 2025 Lorenzo Olmo Marchal
>
> Permission is hereby granted, free of charge, to any person obtaining a copy of this software and associated documentation files (the "Software"), to deal in the Software without restriction, including without limitation the rights to use, copy, modify, merge, publish, distribute, sublicense, and/or sell copies of the Software, and to permit persons to whom the Software is furnished to do so, subject to the following conditions:
>
> The above copyright notice and this permission notice shall be included in all copies or substantial portions of the Software.
>
> THE SOFTWARE IS PROVIDED "AS IS", WITHOUT WARRANTY OF ANY KIND, EXPRESS OR IMPLIED, INCLUDING BUT NOT LIMITED TO THE WARRANTIES OF MERCHANTABILITY, FITNESS FOR A PARTICULAR PURPOSE AND NONINFRINGEMENT. IN NO EVENT SHALL THE AUTHORS OR COPYRIGHT HOLDERS BE LIABLE FOR ANY CLAIM, DAMAGES OR OTHER LIABILITY, WHETHER IN AN ACTION OF CONTRACT, TORT OR OTHERWISE, ARISING FROM, OUT OF OR IN CONNECTION WITH THE SOFTWARE OR THE USE OR OTHER DEALINGS IN THE SOFTWARE.

## Contact

For questions or inquiries, please contact Lorenzo Olmo Marchal at `aolmomarchal@ucsd.edu`.

## References

1.  M. Macenko et al., "A method for normalizing histology slides for quantitative analysis," 2009 IEEE International Symposium on Biomedical Imaging.
2.  Barbano, C. A., & Pedersen, A. (2022). EIDOSLAB/torchstain: v1.2.0-stable. Zenodo.
3.  Chen, R.J., et al. (2024). Towards a general-purpose foundation model for computational pathology. *Nat Med*.
4.  B. A. Schreiber, et al. (2023). Bang
