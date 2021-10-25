# Malawi Seismogenic Source Database - MSSD

The Malawi Seismogenic Source Database (MSSD) is a geospatial database that documents the geometry, slip rate and seismogenic properties (ie earthquake magnitude and frequency) of active faults in Malawi. Each geospatial feature represents a potential earthquake rupture of 'source' and is classified based on its geometry into one of three types:
- section
- fault
- multi-fault

Source types are mutually exclusice, and so if incorporated into a PSHA, they should be assigned relative weightings.

The MSSD is the first seismogenic source database in central and northern Malawi, and represents an update of the South Malawi Seismogenic Source Database (SMSSD; Williams et al., 2021) because it incorporates new active fault traces (Kolawole et al., 2021; Williams et al., submitted - MAFD), new geodetic data and a statistical treatment of uncertainty, within a logic tree approach.

## Citation
Prior to publication please cite this database as:

## Database Design
The MSSD consists of two components:
1) A 3D geometrical model of seismogenic sources in Malawi
2) The mapped trace of each source, with associated source attributes (### Data Table).

## Data Format

### Data Table
Attribute                      | Type        | Description                | Notes
-------------------------------|-------------|----------------------------|-------------------------------------------------------------------------------------------
MSSD_ID                        | integer     | Unique numerical reference ID for each seismic source | ID 00-300 is section rupture <BR>ID 300-500 is fault rupture <BR>ID 600-700 is a multi-fault rupture
name                           | string      |                            | Assigned based on previous mapping or local geographic feature. <BR><BR>For sections and faults, the name of the fault (flt_name) and larger multi-fault (mflt_name) system they are hosted on are given respectively.
basin                          | string      | Basin that source is located within | Used in slip rate calculations
class                          | string      | intrarift or border fault  | 
length (L<sub>s</sub>)                    | real number | straight-line distance in km between fault tips; sum of L<sub>sec</sub> for segmented faults; sum of L<sub>fault</sub> for multi-faults | measured in km to 1 decimal place. Must be greater than 5 km (except for linking sections).
area                           | integer     | Calculated from L<sub>s</sub> multiplied by Eq. 1 or based on fault truncation. | measured in km<sup>2</sup>
strike                         | integer     | Azimuth of straigth line between the fault tips. <BR>azimuth is <180° | Used as input for slip rate estimates in Eq. 2
dip (&delta;)                  | integer     |                            | When no previous measurements are available, a best estimate of 53° is assigned, and no uncertainty is explored for dip in the source geometry. However, in the slip rate calculations, this is randomly varied between 45° and 65°. <BR><BR> No dip is assigned for multi-fault sources, as different participating faults may have different dips.
dip_dir                        | string      | Dip direction: compass quadrant that the fault dips in. | 
slip_type                      | string      | source kinematics (e.g. normal, thrust etc). | All sources in the MSSD are assumed to be normal faults.
slip_rate                      | real number | Mean value from repeating Eq. 2 in Monte Carlo simulations (see manuscript for details). | In mm yr<sup>-1</sup>. All sources in the MSSD are assumed to be normal so is equivalent to dip-slip rate. <BR><BR>Reported to two significant figures.
s_rate_err                     | real number | Slip rate error: 1&sigma; error from Monte Carlo slip rate simlations. | 
mag_lower                      | real number | Lower magnitude estimate. <BR><BR>Calculated from Leonard (2010) scaling relationship (Eq. 4) for L<sub>s</sub> or A<sub>s</sub>, and using lower estimates of C<sub>1</sub> and C<sub>2</sub> constants in Leonard (2010). | Reported to one decimal place.
mag_med                        | real number | Mean magnitude estimate. <BR><BR>Calculated from Leonard (2010) scaling relationship (Eq. 4) for L<sub>s</sub> or A<sub>s</sub>, and using mean estimates of C<sub>1</sub> and C<sub>2</sub> constants in Leonard (2010). | Reported to one decimal place.
mag_upper                      | real number | Upper magnitude estimate. <BR><BR>Calculated from Leonard (2010) scaling relationship (Eq. 4) for L<sub>s</sub> or A<sub>s</sub>, and using upper estimates of C<sub>1</sub> and C<sub>2</sub> constants in Leonard (2010). | Reported to one decimal place.
ri_lower                       | real number | Lower recurrence interval estimate. <BR><BR>Calculated as 1&sigma; below the mean of the Monte Carlo simulations (assuming a log normal distribution). | Reported to two significant figures.
ri_med                         | real number | Mean recurrence interval. <BR><BR>Mean value from log of recurrence interval Monte Carlo simulations. | Reported to two significant figures.
ri_upper                       | real number | Upper recurrence interval estimate. <BR><BR>Calculated as 1&sigma; above the mean of the Monte Carlo simulations (assuming a log normal distribution). | Reported to two significant figures.
MAFD_id                        | list        | List of integers of ID of equivalent structres in the Malawi Active Fault database | Multi-falut sources have multiple ID's.
  
List and brief description of fault geometry, slip rate estimates and earthquake source attributes in the MSSD. Attributes are assigned to each rupture source, with section, fault, and multi-fault ruptures stored in separate files.


