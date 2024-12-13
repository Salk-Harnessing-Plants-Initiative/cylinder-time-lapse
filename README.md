# cylinder-time-lapse

**cylinder-time-lapse** automates the creation of timelapse videos from image datasets. This repository provides easy-to-run Jupyter notebooks for generating MP4 videos from image files, making it accessible to researchers and developers.

---

## Table of Contents
- [Project Overview](#project-overview)
- [Features](#features)
- [Quickstart](#quickstart)
- [File Organization](#file-organization)
  - [Making the H5 Files](#making-the-h5-files)
  - [Making the MP4s](#making-the-mp4s)
- [Contributing](#contributing)
- [License](#license)
- [Contact](#contact)
- [Acknowledgments](#acknowledgments)

---

## Features
- **User-Friendly**: Accessible Jupyter notebooks designed for researchers with varying technical backgrounds.
- **Configurable**: Customizable input/output paths, resolution, playback speed, and overwrite conditions.
- **Efficient Workflow**: Automated generation of H5 and MP4 files for large datasets.
- **Cross-Platform Compatibility**: Works on Windows, macOS, and Linux.
- **Scalable**: Handles large image datasets efficiently.

---

## Quickstart

1. **Navigate to the desired directory**  
   ```bash
   cd path/on/your/computer
   ```

2. **Clone the repository**  
   ```bash
   git clone https://github.com/Salk-Harnessing-Plants-Initiative/cylinder-time-lapse.git
   ```

3. **Navigate into the repository**  
   ```bash
   cd cylinder-time-lapse
   ```

4. **Create the Conda environment**  
   ```bash
   mamba env create -f env.yml
   ```

5. **Activate the environment**  
   ```bash
   mamba activate time_lapse_videos
   ```

6. **Start Jupyter Lab**  
   ```bash
   jupyter lab
   ```

7. **Run the notebooks**  
   - Start by creating the H5 files, then use them to generate MP4 videos.

---

## Making the H5 Files

1. **Organize Files**  
   - Files must be organized by genotype → timepoint → replicate.
   - Each replicate folder should be named using the format `R<replicate_identifier>`.

2. **Configure the Notebook**  
   - Adjust the source and destination directories in the notebook as needed. Example:
     ```python
     base_src_dir = "Arabidopsis"  # Source directory
     base_dst_dir = "output_directory/h5s"  # Destination directory
     ```

### File Organization

The input image files should be structured in a hierarchical directory format as follows. The directory structure is **configurable** based on the provided script variables:

```
<base_src_dir>/
└── <genotype>/
    └── <timepoint>/
        └── <replicate>/
            └── <image>.png
```

#### Configurable Parameters

The following variables allow you to customize the structure:

- **Base Source Directory (`base_src_dir`)**: The root folder containing all genotypes (example: `Sorghum`).
- **Destination Directory (`base_dst_dir`)**: Output folder for H5 files (example: `Sorghum_time_lapse_videos_20240808/h5s_preds_by_frame`).
- **Genotypes (`genotypes`)**: Configurable range of genotype identifiers (example: `1-6`).
- **Timepoints (`days`)**: Configurable range of timepoints in days (example: `1-14`).
- **Number of Images per Timepoint (`img_numbers`)**: Configurable range of images per replicate (example: `1-72`).
- **Overwrite Option (`overwrite`)**: When `True`, existing files will be overwritten.

#### Example Directory Structure

Here’s an example based on the example configuration:

```
Sorghum/
├── 1/
│   ├── 1d/
│   │   └── R1/
│   │       ├── 1.png
│   │       ├── 2.png
│   │       ├── ...
│   │       └── 72.png
│   ├── 2d/
│   │   └── R1/
│   │       ├── 1.png
│   │       ├── ...
│   │       └── 72.png
│   └── 14d/
│       └── R1/
│           ├── 1.png
│           ├── ...
│           └── 72.png
├── 2/
│   ├── 1d/
│   │   └── R2/
│   │       ├── 1.png
│   │       ├── ...
│   │       └── 72.png
│   └── 14d/
│       └── R2/
│           ├── 1.png
│           ├── ...
│           └── 72.png
└── 6/
    ├── 1d/
    │   └── R6/
    │       ├── 1.png
    │       ├── ...
    │       └── 72.png
    └── 14d/
        └── R6/
            ├── 1.png
            ├── ...
            └── 72.png
```

#### Notes
- **Genotype Directories (`<genotype>`)**: Numbered numerically according to the `genotypes` range.
- **Timepoint Folders (`<timepoint>`)**: Use the `<day>d` format for days (e.g., `1d`, `14d`) based on the `days` range.
- **Replicate Folders (`<replicate>`)**: Named as `R<replicate_identifier>` for each replicate.
- **Image Files (`<image>.png`)**: Numbered sequentially according to the `img_numbers` range (e.g., `1.png` to `72.png`).

#### Configuration Example

If you modify the variables as shown below:
```python
base_src_dir = "Arabidopsis"
genotypes = range(1, 4)  # 1 to 3
days = range(1, 10)      # 1 to 9
img_numbers = range(1, 51)  # 1 to 50
```

The structure will adjust accordingly:
```
Arabidopsis/
├── 1/
│   ├── 1d/
│   │   └── R1/
│   │       ├── 1.png
│   │       ├── ...
│   │       └── 50.png
...
└── 3/
    ├── 9d/
        └── R1/
            ├── 1.png
            ├── ...
            └── 50.png
```

Ensure the directory structure matches the configuration parameters for the scripts to run correctly.

### Making the MP4s

1. **Input Configuration**  
   - Specify the location of the H5 files (output from the previous step).

2. **Customization Options**  
   - Adjust resolution and playback speed using the `decimation` and `slowdown_factor`

    ```python
    overwrite = True
    decimation = 2 # Factor used to coarsen the video 
    slowdown_factor = 5  # must be integer >= 1
    ```
    This is used in `render_plant_from_h5`
     ```python
     img = img[::decimate, ::decimate]  # Decimation factor for resolution
     out_video = np.repeat(out_video, slowdown_factor, axis=0)  # Slowdown factor for playback
     ```

---

## Contributing

We welcome contributions to this project! To contribute:
1. Fork the repository.
2. Create a feature branch:
   ```bash
   git checkout -b feature-name
   ```
3. Commit your changes and push to your fork.
4. Open a pull request.

For bug reports or feature requests, please use the [Issues](https://github.com/Salk-Harnessing-Plants-Initiative/cylinder-time-lapse/issues) page.

---

## License

This project is licensed under the BSD 3-Clause License. See the [LICENSE](LICENSE) file for details.

---

## Contact

For questions or support, please contact:  
**[Elizabeth Berrigan](eberrigan@salk.edu)**  

---

## Acknowledgments

- **Salk Harnessing Plants Initiative**: For providing support and resources for this project.
- **Contributors**: Thanks to all contributors for their invaluable work.
- **Open Source Tools**: This project relies on many open-source libraries and tools.

---