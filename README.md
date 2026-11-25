<h1 align="center">T2w-to-T1w Registration</h1>

<p align="center">
  Registers a T2-weighted image to a T1-weighted reference with ANTs using translation, rigid, affine and optional SyN stages, outputting the transforms and the registered T2w.
</p>

<p align="center">
  <a href="https://github.com/brainlife/abcd-spec"><img src="https://img.shields.io/badge/ABCD_Spec-v1.1-green.svg" alt="ABCD Spec v1.1"></a>
  <a href="https://doi.org/10.25663/brainlife.app.877"><img src="https://img.shields.io/badge/Brainlife-brainlife.app.877-blue.svg" alt="Run on brainlife.io"></a>
  <a href="LICENSE"><img src="https://img.shields.io/badge/License-see_LICENSE-lightgrey.svg" alt="License"></a>
</p>

## At a glance

<!-- brainlife-app:begin (generated from the App manifest; edit the manifest, not this block) -->

> **Registers a T2-weighted image to a T1-weighted reference with ANTs using translation, rigid, affine and optional SyN stages, outputting the transforms and the registered T2w.**

Runs antsRegistration from the moving image to the fixed image up to the selected transformation stage, with the pyramid depth set by settings, and applies the result to the moving image. Use it to bring a subject's T2w into its T1w space (or for inter-subject normalisation). The README describes the T1w-to-T1w variant of the same code.

| | |
|---|---|
| **Inputs** | `neuro/anat/t2w` · `neuro/anat/t1w` |
| **Outputs** | `neuro/transform/nifti` · `neuro/anat/t2w` |
| **Container** | `brainlife/ants:2.2.0-1bc` |
| **Resources** | 1 CPUs · 2 h walltime |
| **Run it** | [doi.org/10.25663/brainlife.app.877](https://doi.org/10.25663/brainlife.app.877) |

#### Inputs

| Input | Datatype | Required | Description |
|---|---|---|---|
| `t2_moving` | `neuro/anat/t2w` | yes | T2-weighted image to register (moving). |
| `t1_fixed` | `neuro/anat/t1w` | yes | T1-weighted image used as the fixed reference. |

#### Outputs

| Output | Datatype | Description |
|---|---|---|
| `transformations` | `neuro/transform/nifti` | ANTs affine matrix and warp fields from the T2w to the T1w space. |
| `transformed` | `neuro/anat/t2w` | T2-weighted image resampled into the T1w reference space. |

<details>
<summary><b>Parameters</b> (2)</summary>

| Parameter | Type | Default | Description |
|---|---|---|---|
| `settings` | enum | `4` | The `settings` parameter controls the depth of the multiresolution (pyramidal) registration strategy used by ANTs. Higher settings correspond to more levels in the registration pyramid, starting from coarse alignment and progressively refining toward finer spatial correspondence. Options: `1`, `2`, `3`, `4`. |
| `transformation` | enum | `nonlinear` | Highest registration stage to run: translation, rigid, affine or nonlinear (SyN); each stage includes the previous ones. Options: `translation`, `rigid`, `affine`, `nonlinear`. |

</details>

<!-- brainlife-app:end -->

## Running the App

### On brainlife.io

Open the App at [doi.org/10.25663/brainlife.app.877](https://doi.org/10.25663/brainlife.app.877), choose `neuro/anat/t2w`, `neuro/anat/t1w` from your project, set the parameters and press **Execute**. The results are saved to your project as `neuro/transform/nifti`, `neuro/anat/t2w`.

### Locally

You need [Singularity/Apptainer](https://apptainer.org/) (the App runs in `brainlife/ants:2.2.0-1bc`), [`jq`](https://jqlang.github.io/jq/).

1. Clone this repository.
2. Create `config.json` with the paths to your inputs and the parameters:

   ```json
   {
       "t2": "/path/to/t2_moving/t2",
       "t1_fixed": "/path/to/t1_fixed/t1_fixed",
       "settings": "4",
       "transformation": "nonlinear"
   }
   ```

3. Run `./main`.

## Troubleshooting

- **Error: No valid input found in config.json**: Provide the moving image input.

## Citing

If you use this App, please cite it, the software it builds on and brainlife.io:

- T2w-to-T1w Registration. brainlife.io App. [doi:10.25663/brainlife.app.877](https://doi.org/10.25663/brainlife.app.877)
- Avants, B. B., Tustison, N. J., Song, G., Cook, P. A., Klein, A., & Gee, J. C. (2011). A reproducible evaluation of ANTs similarity metric performance in brain image registration. Neuroimage, 54(3), 2033-2044.
- Hayashi, S., Caron, B. A., Heinsfeld, A. S., ... & Pestilli, F. (2024). brainlife. io: a decentralized and open-source cloud platform to support neuroscience research. Nature methods, 21(5), 809-813. ---
- Avants et al. A reproducible evaluation of ANTs similarity metric performance in brain image registration. *NeuroImage* 54:2033-2044 (2011). [doi:10.1016/j.neuroimage.2010.09.025](https://doi.org/10.1016/j.neuroimage.2010.09.025)
- Hayashi S, Caron BA, Heinsfeld AS, et al. brainlife.io: a decentralized and open-source cloud platform to support neuroscience research. *Nature Methods* 21:809–813 (2024). [doi:10.1038/s41592-024-02237-2](https://doi.org/10.1038/s41592-024-02237-2)
- Avesani P, McPherson B, Hayashi S, et al. The open diffusion data derivatives, brain data upcycling via integrated publishing of derivatives and reproducible open cloud services. *Scientific Data* 6:69 (2019). [doi:10.1038/s41597-019-0073-y](https://doi.org/10.1038/s41597-019-0073-y)

## Authors

**Gabriele Amorosino**  
(email:

---

## License

See [LICENSE](LICENSE).
