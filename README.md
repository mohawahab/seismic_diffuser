# How to Execute the SEG-Y Volume Processing Notebook

This guide explains how to set up the environment, install dependencies, and execute the Jupyter Notebook for processing SEG-Y seismic data.

## Step 1: Create a Virtual Environment

To isolate dependencies, create a virtual environment using Python:

```bash
python -m venv venv
source venv/bin/activate  # On Windows, use `venv\Scripts\activate`
```

## Step 2: Install Required Packages

Install the required Python libraries listed in `requirements.txt`:

```bash
pip install -r requirements.txt
```

## Step 3: Understand the Data Directory

The data directory structure is defined in `env.json`. The `data_utils.py` script will ensure that the required data is downloaded and organized correctly. The structure should look like this after setup:

```
data/
  raw/
    labels_entire_volume.npy
    seismic_entire_volume.npy
    Faults/
      Polygons 1
      Polygons 1-UNIQ1
      Polygons 1-UNIQ1.crsmeta.xml
      ...
    Horizons/
      ...
```

## Step 4: Download Data Automatically
Note: Running `segy_notebook_executed.ipynb` will download the data for you if it isn't downloaded already, this section explain how it is done.
The `data_utils.py` script will handle downloading and organizing the data. It uses the `env.json` file to locate the data paths and URLs. If the data is missing, it will:

1. Create the required directories.
2. Download the data from the specified URL.
3. Extract and validate the data files.

Ensure that `env.json` is correctly configured with the following structure:

```json
{
  "data": {
    "raw": {
      "path": "./data/raw",
      "url": "<data-download-url>",
      "compression": "zip",
      "files": {
        "labels": "labels_entire_volume.npy",
        "processed_seismic": "seismic_entire_volume.npy"
      }
    }
  }
}
```

## Step 5: Run the Jupyter Notebook

Launch the Jupyter Notebook server and open the `segy_notebook_executed.ipynb` file:

```bash
jupyter notebook segy_notebook_executed.ipynb
```

## Step 6: Execute the Notebook

Follow the cells in the notebook to process your SEG-Y data. The notebook includes functions for reading SEG-Y files, parsing headers, building seismic volumes, and visualizing inline slices.