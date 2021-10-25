# Malawi Seismic Source Database - MSSD


## Citation
Prior to publication please cite this database as:


## Data Format

### Data Table
Attribute                      | Type    | Description                | Notes
MSSD_ID                        | integer | Unique numerical reference ID for each seismic source | ID 00-300 is section rupture
ID 300-500 is fault rupture
ID 600-700 is a multi-fault rupture
name                           | string  |                            | Assigned based on previous mapping or local geographic feature.
For sections and faults, the name of the fault (flt_name) and larger multi-fault (mflt_name) system they are hosted on are given respectively.
basin                          | string  | Basin that source is located within | Used in slip rate calculations

