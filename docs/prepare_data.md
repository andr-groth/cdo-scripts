# Prepare data

The `prepare_data.sh` script is used to process netCDF files in a given folder. It performs three main steps: creating anomalies, calculating ensemble EOFs (Empirical Orthogonal Functions), and obtaining individual PCs (Principal Components). The resulting anomalies, EOFS, and PCs are saved in specific subfolders within the input `FILEPATH`.

## Usage

To use the script, run the following command in the terminal:

```bash
./prepare_data.sh CONFIGFILE NEOFS FILEPATH
```

Arguments:

- `CONFIGFILE`: The path to the configuration file that provides parameters for creating anomalies.
- `NEOFS`: The number of EOFs to calculate.
- `FILEPATH`: The path to the folder containing the netCDF files to be processed.

## Script Steps

1. **Create Anomalies**
    - The script calls the `get_anom.sh` script to create anomalies for each input netCDF file.
    - The path to the configuration file (`CONFIGFILE`) and the netCDF files in `FILEPATH` are provided as arguments.
    - Anomalies are created for each input file using the specified parameters from the configuration file.

2. **Calculate Ensemble EOFs**
    - The script calls the `get_eofs.sh` script to calculate ensemble EOFs and eigenvalues.
    - The number of EOFs to calculate is determined by the `NEOFS` argument.
    - The anomalies created in the previous step are used as input.

3. **Obtain Individual PCs**
    - The script calls the `get_pcs.sh` script to obtain individual PCs by projecting the anomalies onto the ensemble EOFs.

## Output
The resulting data files are saved in the following subfolders:

- Anomalies: The resulting anomalies are saved in a subfolder named `anom` within `FILEPATH`.
- Ensemble EOFs: The calculated EOFs are saved in a subfolder named `anom/pcs` within `FILEPATH`.
- PCs: The individual PCs are saved in a subfolder named `anom/pcs` within `FILEPATH`.

## Example

Suppose we want to process netCDF files located in the folder `/data/files`. We have a configuration file named `config.sh`, and we want to calculate 10 EOFs.

The command to run the script would be:

```bash
./prepare_data.sh config.sh 10 /data/files
```

The resulting data files are:

- Anomalies: `/data2/files/anom/anom_*.nc`.
- Ensemble EOFs: `/data2/files/anom/pcs/eofs.nc`.
- PCs: `/data2/files/anom/pcs/pcs_*.nc`.