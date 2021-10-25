# Malawi Seismic Source Database - MSSD


## Citation
Prior to publication please cite this database as:


## Data Format

### Data Table
Attribute                      | Type        | Description                | Notes
-------------------------------|-------------|----------------------------|-------------------------------------------------------------------------------------------
MSSD_ID                        | integer     | Unique numerical reference ID for each seismic source | ID 00-300 is section rupture <BR>ID 300-500 is fault rupture <BR>ID 600-700 is a multi-fault rupture
name                           | string      |                            | Assigned based on previous mapping or local geographic feature. <BR><BR>For sections and faults, the name of the fault (flt_name) and larger multi-fault (mflt_name) system they are hosted on are given respectively.
basin                          | string      | Basin that source is located within | Used in slip rate calculations
class                          | string      | intrarift or border fault  | 
length (L<sub>s</sub>)                    | real number | straight-line distance in km between fault tips; sum of L<sub>sec/sub> for segmented faults; sum of L<sub>fault/sub> for multi-faults | measured in km to 1 decimal place. Must be greater than 5 km (except for linking sections).
area                           | integer     | Calculated from L<sub>s</sub> multiplied by Eq. 1 or based on fault truncation. | measured in km<sup>2</sup>
strike                         | integer     | Azimuth of straigth line between the fault tips. <BR>azimuth is <180° | Used as input for slip rate estimates in Eq. 2
dip (&delta)                   | integer     |                            | When no previous measurements are available, a best estimate of 53° is assigned, and no uncertainty is explored for dip in the source geometry. However, in the slip rate calculations, this is randomly varied between 45° and 65°. <BR><BR> No dip is assigned for multi-fault sources, as different participating faults may have different dips.
dip_dir                        | string      | Dip direction: compass quadrant that the fault dips in. | 
slip_type                      | string      | source kinematics (e.g. normal, thrust etc). | All sources in the MSSD are assumed to be normal faults.

  



