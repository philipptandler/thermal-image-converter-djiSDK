# Thermal Image Converter
Original Author: Alexis Suero (alexis.esmb@gmail.com).  
Enhancements: Philipp Tandler (philipp.tandler@protonmail.ch).

This repository contains a Python script that converts thermal JPEG images captured by DJI drones into TIFF format containing a single layer with temperature values in Celsius. The converted images are saved in the "output_images" folder.

## Table of Contents
- [Requirements](#requirements)
- [Installation](#installation)
- [Usage](#usage)
- [Example](#example)
- [Author](#author)

## Requirements
- `DJI Thermal SDK` (not included in repository)
- `exiftool` (included in the repository, consider downloading the latest version)
- Python 3.11.x or later
- The following Python libraries:
  - `rasterio`
  - `dji_thermal_sdk`
  - `tqdm`

## Installation
1. **Clone the repository:**

    ```sh
    git clone https://github.com/philipptandler/thermal-image-converter-djiSDK.git
    cd thermal-image-converter-djiSDK
    ```
2. **Create a virtual environment:**

   - Create a new environment with Python 3.12.4 or later:
   ```sh
    conda create --name thermConv python=3.12.4
   ```
       
3. **Install the required Python libraries:**

   - Install `dji_thermal_sdk` package:
   ```sh
    pip install dji_thermal_sdk
   ```

   - Install `rasterio` package:
   ```sh
    pip install rasterio
   ```

    - Install `tqdm` package:
   ```sh
    pip install tqdm
   ```

4. **Make sure ExifTool is available to your computer:**
    - You can download `exiftool` from [here](https://exiftool.org/) (recommended) or use the zipped version in `tools\exiftool-13.40_64` as fallback. After download or extraction, it should look like this:
    ```
    exiftool-version_64/
    ├── exiftool_files/
    ├── exiftool.exe (you might have to remane it from exiftool(-k).exe to exiftool.exe)
    └── README.txt
    ```

    - You can place `exiftool` either in a general location of your computer (recommended) or in the root directory of the repository:

        - To run exiftool from a general location, place place the `exiftool` folder in a location such as `C:\Users\username\exiftool-version_64` or (if you have admin permissions) in your program files `C:\Program Files\exiftool-version_64`. Make sure to add the `exiftool` folder in your path variables (Windows Key -> Edit environment variables -> Path -> Edit, where you add the location, e.g. `%USERPROFILE%\exiftool-version_64` or `C:\Program Files\exiftool-version_64`).

        - Alternatively, you can place the `exiftool_files/` folder and the `exiftool.exe` directly in the root directory of the repository. Be aware that this will add roughly 40 MB storage space to your repository. You can avoid this by adjusting the `.gitignore` file to exclude `exiftool_files/*` and `exiftool.exe*`.

    - To test the installation, run from the project root (or anywhere really) `exiftool`+Enter, which should display the documentation of `exiftool`. Press `q` to exit.

    - To see where the exiftool is located, use:
    ```sh
    where exiftool
    ```


5. **Download `DJI Thermal SDK` and place its files in `dji_thermal_sdk` folder:**
    - You can download `DJI Thermal SDK` from [here](https://www.dji.com/global/downloads/softwares/dji-thermal-sdk).

    - `dji_thermal_sdk` folder should look like:
      ```
      dji_thermal_sdk/
      ├── dataset/
      ├── doc/
      ├── sample/
      ├── tsdk-core/
      ├── utility/
      ├── History.txt
      ├── License.txt
      └── Readme.md
      ```
      Place it in the root directory.

6. **Check your setup**
    - Your root directory should look similar to this:
      ```
      thermal-image-converter-djiSDK/
      ├── .git/
      ├── dji_thermal_sdk/
      ├── (exiftool_files/, if you decide to work with local exiftool)
      ├── tools/
      ├── .gitignore
      ├── dji_thermal_converter.py
      ├── (exiftool.exe, if you decide to work with local exiftool)
      ├── LICENSE
      ├── Readme.md
      ├── sort_images.py
      └── wrapper.py
      ```
    - To test the exiftool installation, run from the project root:
    ```sh
    exiftool
    ```
    - This should display the documentation of `exiftool`. Press `q` to exit.

## Usage
This is the most basic workflow:
1. **Prepare your input images:**
    - Place all thermal JPEG images (with `_T.JPG` suffix) in the `input_images` folder, create if required.

2. **Run the script:**
    ```sh
    python dji_thermal_converter.py
    ```

3. **Find your converted images:**
    - The converted TIFF images will be saved in the `output_images` folder.

You can also specify the input directory:
1. **Run the script:**
    ```sh
    python dji_thermal_converter.py your/directory/with/JPEGfiles
    ```

2. **Find your converted images:**
    - The converted TIFF images will be saved in the `your/directory/with/JPEGfiles/output_images` folder.

As well as specify an input and output directory:
1. **Run the script:**
    ```sh
    python dji_thermal_converter.py your/directory/with/JPEGfiles your/directory/for/the/outputfiles
    ```

2. **Find your converted images:**
    - The converted TIFF images will be saved in the `your/directory/for/the/outputfiles` folder.

If you have many directories to process, you can use the `wrapper.py` script and add the directories you want to batch process:
1. **Run the script:**
    ```sh
    python wrapper.py "some/particular/input/directory/with/JPEGfiles" "some/other/input/directory/with/JPEGfiles" "some/third/input/directory/with/JPEGfiles"
    ```

2. **Find your converted images:**
    - The converted TIFF images will be saved in the `outputfiles` folder for each speciefied directory.

The script `sort_images.py` is useful when you have a folder with hundreds of both Thermal JPG files (`*_T.JPG`) and Wide angle RGB files (`*_W.JPG`) and you want to sort them in separate folders:
1. **Run the script:**

    ```sh
    python sort_images.py path\to\folder\you\want\to\sort
    ```

## Example
Here's an example of how to use the script:
1. **Place your thermal JPEG images in the `input_images` folder:**
    ```
    input_images/
    ├── image1_T.JPG
    ├── image2_T.JPG
    └── image3_T.JPG
    ```

2. **Run the script:**
    ```sh
    python dji_thermal_converter.py
    ```

3. **Check the `output_images` folder for the converted TIFF images:**
    ```
    output_images/
    ├── image1.tif
    ├── image2.tif
    └── image3.tif
    ```

## License
This project is licensed under the GNU General Public License v3.0.
