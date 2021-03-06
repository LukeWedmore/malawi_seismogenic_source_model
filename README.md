# Malawi Seismogenic Source Model - MSSM

[![DOI](https://zenodo.org/badge/DOI/10.5281/zenodo.5599616.svg)](https://doi.org/10.5281/zenodo.5599616)

The Malawi Seismogenic Source Model (MSSM) is a geospatial database that documents the geometry, slip rate and seismogenic properties (ie earthquake magnitude and frequency) of active faults in Malawi. Each geospatial feature represents a potential earthquake rupture of 'source' and is classified based on its geometry into one of three types:
- section
- fault
- multi-fault

Source types are mutually exclusice, and so if incorporated into a PSHA, they should be assigned relative weightings.

The MSSD is the first seismogenic source database in central and northern Malawi, and represents an update of the South Malawi Seismogenic Source Database (SMSSD; Williams et al., 2021a) because it incorporates new active fault traces (Kolawole et al., 2021; [Williams et al., 2021b]; [Williams et al., 2022]; the [MAFD]), new geodetic data ([Wedmore et al., 2021]) and a statistical treatment of uncertainty, within a logic tree approach.

The seismogenic sources in this model are adapted from the faults in the Malawi Active Fault Database ([Williams et al., 2021b]; [Williams et al., 2022]).

## Citation
Prior to publication please cite this database using the following two references:
Williams, J. N., Wedmore, L. N .J., Fagereng, Å., Werner, M. J., Biggs, J., Mdala, H., Kolawole, F., Shillington, D. J., Dulanya, Z., Mphepo, F., Chindandali, P., Wright, L. J. M.., Scholz, C. A. Geological and geodetic constraints on the seismic hazard of Malawi's active faults: the Malawi Seismogenic Source Model (MSSM). _Manuscript submitted to Natural Hazards and Earth System Sciences_

Williams, Jack N., Wedmore, Luke N. J., Fagereng, Åke, Werner, Maximilian J., Biggs, Juliet, Mdala, Hassan, Kolawole, Folarin, Shillington, Donna J., Dulanya, Zuze, Mphepo, Felix, Chindandali, Patrick R. N., Wright, Lachlan J. M., & Scholz, Christopher A. (2021). Malawi Seismogenic Source Model [Data set]. Zenodo. https://doi.org/10.5281/zenodo.5599616

## Model Design and File Formats
The MSSD is a geospatial database that consists of two separate components:
1) A 3D geometrical model of fault seismogenic sources in Malawi
2) The mapped trace of each source in a GIS vector format, with associated source attributes (Data Table).

Each fault is associated with a source in the 3D geometrical model that is listed in a  comma-separated-values (csv) file. The sections, faults and multi-faults that make up the individual seismogenic sources are described in separate geospatial files that describe the map-view geometry and metadata that control each sources earthquake magnitude and frequency for seismic hazard purposes. 
  
The sections, faults and multi-faults in this database are provided in a variety of GIS vector file formats. [GeoJSON] is the version of record, and any changes should be made in this version before they are converted to other file formats using the script in the repository that uses the [GDAL] tool [ogr2ogr] (the script is adapted from https://github.com/cossatot/central_am_carib_faults/blob/master/convert.sh - we thank Richard Styron for making this publicly available). The other versions available are [ESRI ShapeFile], [KML], [GMT], and [GeoPackage].

### Data Table
Attribute                      | Type        | Description                | Notes
-------------------------------|-------------|----------------------------|-------------------------------------------------------------------------------------------
MSSM_ID                        | integer     | Unique numerical reference ID for each seismic source | ID 00-300 is section rupture <BR>ID 300-500 is fault rupture <BR>ID 600-700 is a multi-fault rupture
name                           | string      |                            | Assigned based on previous mapping or local geographic feature. <BR><BR>For sections and faults, the name of the fault (flt_name) and larger multi-fault (mflt_name) system they are hosted on are given respectively.
basin                          | string      | Basin that source is located within | Used in slip rate calculations
class                          | string      | intrarift or border fault  | 
length (L<sub>s</sub>)                    | real number | straight-line distance in km between fault tips; sum of L<sub>sec</sub> for segmented faults; sum of L<sub>fault</sub> for multi-faults | measured in km to 1 decimal place. Must be greater than 5 km (except for linking sections).
area                           | integer     | Calculated from L<sub>s</sub> multiplied by Eq. 1 or based on fault truncation. | measured in km<sup>2</sup>
strike                         | integer     | Azimuth of straigth line between the fault tips. <BR>azimuth is <180° | Used as input for slip rate estimates in Eq. 2
dip_lower                      | integer     | Lower range of dip value   | When no previous measurements of dip are available, a nominal value of 45° is used.
dip_int                        | integer     | Intermediate dip value     | In the MSSM geometrical model, only the intermediate measurements is considered. When no previous measurements of are available, a nominal value of 53° is assigned. <BR><BR> No dip is assigned for multi-fault sources, as different participating faults may have different dips.
dip_upper                      | integer     | Upper range of dip value   | When no previous measurements of dip are availabe, a nominal value of 65° is used.
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
MAFD_id                        | list        | List of integers of ID of equivalent structures in the [Malawi Active Fault Database] | Multi-fault sources have multiple ID's.
  
List and brief description of fault geometry, slip rate estimates and earthquake source attributes in the MSSD. Attributes are assigned to each rupture source, with section, fault, and multi-fault ruptures stored in separate files. For equations used we refer people to the original manuscript.

  
## Version Control

This version is intended to be "Live" and as such we encourage edits of the GeoJSON file and the submission of pull requests. Please contact Jack Williams <jack.williams@otago.ac.nz> Luke Wedmore <luke.wedmore@bristol.ac.uk> or Hassan Mdala <mdalahassan@yahoo.com> for information, other requests or if you find any errors within the database.
  
It is the intention that future versions of this database will include fault slip rates that have been determined from direct geological methods (e.g. offset stratigraphy that has been dated) rather than the systems based approach that is currently used.
  
  
### References

  Kolawole, F., Firkins, M. C., Al Wahaibi, T. S., Atekwana, E. A., & Soreghan, M. J. (2021a). Rift Interaction Zones and the Stages of Rift Linkage in Active Segmented Continental Rift Systems. _Basin Research_. https://doi.org/10.1111/bre.12592

  Leonard, M. (2010). Earthquake fault scaling: Self-consistent relating of rupture length, width, average displacement, and moment release. _Bulletin of the Seismological Society of America_, 100(5A), 1971-1988. https://doi.org/10.1785/0120090189

  Wedmore, L. N. J., Biggs, J., Floyd, M., Fagereng, Å., Mdala, H., Chindandali, P. R. N., et al. (2021). Geodetic constraints on cratonic microplates and broad strain during rifting of thick Southern Africa lithosphere. _Geophysical Research Letters_. 48(17), e2021GL093785. https://doi.org/10.1029/2021GL093785

  Williams, J. N., Mdala, H., Fagereng, Å., Wedmore, L. N. J., Biggs, J., Dulany, Z., et al. (2021a). A systems-based approach to parameterise seismic hazard in regions with little historical or instrumental seismicity: Active fault and seismogenic source databases for southern Malawi. Solid Earth, 12(1), 187–217. https://doi.org/10.5194/se-12-187-2021
  
  Williams, J. N., Wedmore, L. N. J., Scholz, C. A., Kolawole, F., Wright, J. M., Shillington, D. J., Fagereng, Å., Biggs, J., Mdala, H., Dulanya, Z., Mphepo, F., Chindandali, P. R. N., Werner, M. J. (2021b). Malawi Active Fault Database. Hosted on _Zenodo_: https://doi.org/10.5281/zenodo.5507190
  
  Williams, J. N., Wedmore, L. N. J., Scholz, C. A., Kolawole, F., Wright, J. M., Shillington, D. J., Fagereng, Å., Biggs, J., Mdala, H., Dulanya, Z., Mphepo, F., Chindandali, P. R. N., Werner, M. J. (2022). The Malawi Active Fault Database: An Onshore-Offshore Database for Regional Assessment of Seismic Hazard and Tectonics Evolution. _Geochemistry, Geophysics, Geosystems_, 23(5), e2022GC010425.  https://doi.org/10.1029/2022GC010425 


  
[MAFD]: https://doi.org/10.5281/zenodo.5507190
[Malawi Active Fault Database]: https://doi.org/10.5281/zenodo.5507190
[GeoJSON]: http://geojson.org/
[GeoPackage]: https://www.geopackage.org/
[ESRI ShapeFile]: https://support.esri.com/en/white-paper/279
[Global Earthquake Model Global Active Faults Database]: https://github.com/cossatot/gem-global-active-faults
[GEM-GAFD]: https://github.com/cossatot/gem-global-active-faults
[ogr2ogr]: https://gdal.org/programs/ogr2ogr.html
[GDAL]: https://gdal.org/
[KML]: https://earth.google.com
[GMT]: https://www.generic-mapping-tools.org/
[Wedmore et al., 2021]: https://doi.org/10.1029/2021GL093785
[Williams et al., 2021b]: https://zenodo.org/record/5507190#.YrxpuFl7mN8
[Williams et al., 2022]: https://doi.org/10.1029/2022GC010425
