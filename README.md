<h1 align="center">FSLmaths-app</h1>

<p align="center">
  Combines one ROI from each of two ROI sets with FSL fslmaths (add, subtract, multiply, divide or mask), for example to remove a lesion from a region of interest.
</p>

<p align="center">
  <a href="https://github.com/brainlife/abcd-spec"><img src="https://img.shields.io/badge/ABCD_Spec-v1.1-green.svg" alt="ABCD Spec v1.1"></a>
  <a href="https://doi.org/10.25663/brainlife.app.680"><img src="https://img.shields.io/badge/Brainlife-brainlife.app.680-blue.svg" alt="Run on brainlife.io"></a>
  <a href="LICENSE"><img src="https://img.shields.io/badge/License-see_LICENSE-lightgrey.svg" alt="License"></a>
</p>

## At a glance

<!-- brainlife-app:begin (generated from the App manifest; edit the manifest, not this block) -->

> **Combines one ROI from each of two ROI sets with FSL fslmaths (add, subtract, multiply, divide or mask), for example to remove a lesion from a region of interest.**

Copies the named ROI from each input ROI directory and runs fslmaths <roi_1> -<function> <roi_2>, writing the result as a new ROI; with sub the result is clipped to 0-1 so it stays binary. Use it to mask an ROI by a lesion or to merge or intersect ROIs. Both ROIs must be on the same voxel grid; with sub the order of inputs matters.

| | |
|---|---|
| **Inputs** | `neuro/rois` ×2 |
| **Outputs** | `neuro/rois` |
| **Container** | `brainlife/fsl:5.0.11` |
| **Resources** | 4 GB memory · 0.25 h walltime |
| **Run it** | [doi.org/10.25663/brainlife.app.680](https://doi.org/10.25663/brainlife.app.680) |

#### Inputs

| Input | Datatype | Required | Description |
|---|---|---|---|
| `rois1` | `neuro/rois` | yes | If you want to subtract, the order of inputs matters (first ROI is manipulated). For other functions it does not. |
| `rois2` | `neuro/rois` | yes | ROI directory containing the second ROI (roi_2), e.g. a lesion mask, applied to the first. |

#### Outputs

| Output | Datatype | Description |
|---|---|---|
| `output` | `neuro/rois` | ROI directory with copies of both input ROIs and the result <output_roi_name>.nii.gz. |

<details>
<summary><b>Parameters</b> (4)</summary>

| Parameter | Type | Default | Description |
|---|---|---|---|
| `roi_1` | string |  | File name (without .nii.gz) of the ROI to take from the first ROI input. |
| `function` | enum | `sub` | fslmaths operation applied as roi_1 -<function> roi_2: add, sub (subtract, then clipped to 0-1), mul, div or mas (mask). Options: `add`, `sub`, `mul`, `div`, `mas`. |
| `roi_2` | string |  | File name (without .nii.gz) of the ROI to take from the second ROI input. |
| `output_roi_name` | string |  | File name (without .nii.gz) for the resulting ROI. |

</details>

<!-- brainlife-app:end -->

## Running the App

### On brainlife.io

Open the App at [doi.org/10.25663/brainlife.app.680](https://doi.org/10.25663/brainlife.app.680), choose `neuro/rois`, `neuro/rois` from your project, set the parameters and press **Execute**. The results are saved to your project as `neuro/rois`.

### Locally

You need [Singularity/Apptainer](https://apptainer.org/) (the App runs in `brainlife/fsl:5.0.11`), [`jq`](https://jqlang.github.io/jq/).

1. Clone this repository.
2. Create `config.json` with the paths to your inputs and the parameters:

   ```json
   {
       "rois_1_loc": "/path/to/rois1/rois_1_loc",
       "rois_2_loc": "/path/to/rois2/rois_2_loc",
       "roi_1": "",
       "function": "sub",
       "roi_2": "",
       "output_roi_name": ""
   }
   ```

3. Run `./main`.

## Citing

If you use this App, please cite it, the software it builds on and brainlife.io:

- FSLmaths-app. brainlife.io App. [doi:10.25663/brainlife.app.680](https://doi.org/10.25663/brainlife.app.680)
- Jenkinson et al. FSL. *NeuroImage* 62:782-790 (2012). [doi:10.1016/j.neuroimage.2011.09.015](https://doi.org/10.1016/j.neuroimage.2011.09.015)
- Hayashi S, Caron BA, Heinsfeld AS, et al. brainlife.io: a decentralized and open-source cloud platform to support neuroscience research. *Nature Methods* 21:809–813 (2024). [doi:10.1038/s41592-024-02237-2](https://doi.org/10.1038/s41592-024-02237-2)
- Avesani P, McPherson B, Hayashi S, et al. The open diffusion data derivatives, brain data upcycling via integrated publishing of derivatives and reproducible open cloud services. *Scientific Data* 6:69 (2019). [doi:10.1038/s41597-019-0073-y](https://doi.org/10.1038/s41597-019-0073-y)

## Authors

- Hanna Willis
- Brad Caron

## License

See [LICENSE](LICENSE).
