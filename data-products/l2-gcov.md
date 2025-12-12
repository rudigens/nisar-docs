# Geocoded Polarimetric Covariance

## Product Overview

The GCOV product is an L2 product derived from the L1 Range Doppler Single Look Complex (RSLC) product, providing terrain-corrected polarimetric covariance projected onto a predefined UTM or polar stereographic projection system grid. RSLC radar samples, organized as a polarimetric scattering vector, are cross-correlated with the scattering vector’s conjugate transpose, originating the polarimetric covariance matrix expressed in the same grid as the RSLC range-Doppler grid. 

The magnitude of the resulting polarimetric covariance terms is strongly affected by the topography, with areas facing the sensor becoming brighter and areas away from the sensor turning darker in the images, biasing covariance measurements. To reduce the effect of the topography, an area-based radiometric terrain correction (RTC) is applied over the covariance terms, normalizing the backscatter coefficient beta0 to gamma0. The normalized covariance terms are then geocoded onto the output grid using area-based adaptive multi-looking. 

```{figure} /assets/nisar-gcov.png
:label: covariance
:alt: Covariance polarimetric matrix elements
:width: 400px
:align: left

Covariance polarimetric matrix elements
```

Since the polarimetric covariance matrix is Hermitian, only the upper triangular covariance terms are provided. The diagonal terms of the polarimetric covariance matrix (highlighted in darker gray) are real-valued (HHHH, HVHV, VHVH, and VVVV, or RHRH and RVRV), representing the radar backscatter associated with each polarimetric channel. The off-diagonal terms of the polarimetric covariance matrix (highlighted in lighter gray) are complex-valued (HHHV, HHVH, HHVV, HVVH, and VHVV, or RHRV) and may or may not be present depending on the GCOV processing mode.

## Finding Data

{button}`Find in Vertex<https://search.asf.alaska.edu/#/?dataset=NISAR&sciProducts=GCOV>`

{button}`Find in Earthdata Search<https://search.earthdata.nasa.gov/search?q=nisar_l2_gcov_&ac=true>`

## Product Specification

{button}`Product Specification<https://nisar.asf.earthdatacloud.nasa.gov/NISAR-SAMPLE-DATA/DOCS/NISAR_D-102274_RevE_NASA_SDS_Product_Specification_L2_GCOV_Nov8_2024_w-sigs.pdf>`

## Data Layers

A GCOV data product includes the following raster data sets. For more information, see section 4.3 of the [product specification](#product-specification).

### Geocoded Polarimetric Covariance Terms
```
/science/LSAR/GCOV/grids/frequency[A|B]/HHHH
/science/LSAR/GCOV/grids/frequency[A|B]/HVHV
/science/LSAR/GCOV/grids/frequency[A|B]/HHHV
/science/LSAR/GCOV/grids/frequency[A|B]/HHVH
/science/LSAR/GCOV/grids/frequency[A|B]/HHVV
/science/LSAR/GCOV/grids/frequency[A|B]/HVVH
/science/LSAR/GCOV/grids/frequency[A|B]/HVVV
/science/LSAR/GCOV/grids/frequency[A|B]/VVVV
/science/LSAR/GCOV/grids/frequency[A|B]/VHVH
/science/LSAR/GCOV/grids/frequency[A|B]/VHVV
/science/LSAR/GCOV/grids/frequency[A|B]/RHRH
/science/LSAR/GCOV/grids/frequency[A|B]/RVRV
/science/LSAR/GCOV/grids/frequency[A|B]/RHRV
```

The primary data elements of the GCOV product are the images of the geocoded polarimetric covariance terms.

The diagonal terms (HHHH, HVHV, VVVV, VHVH, RHRH, RVRV) are real-valued and represent the radar backscatter.

The remaining terms (HHHV, HHVH, HHVV, HVVH, HVVV, VHVV, RHRV) are complex valued and relate to the electrical and geometric properties of the observed surface.

Which frequencies and polarizations are available in a particular GCOV data product will vary based on the acquisition mode of the satellite used to collect the data.

For more information on NISAR polarimetry, see [TODO](https://science.nasa.gov/mission/nisar/polarimetry/)

### Number of Looks

`/science/LSAR/GCOV/grids/frequency[A|B]/numberOfLooks`

The GCOV terms are obtained from the geocoding of the RSLC product polarimetric covariance terms using an adaptive area-based multi-looking algorithm. The multi-looking window and number of averaged looks vary with the topography and radar geometry. The number of looks layer provides the number of looks used for computing each GCOV term sample. 

### Mask

`/science/LSAR/GCOV/grids/frequency[A|B]/mask`

The mask layer provides information about the averaging ensemble of radar samples that originated the GCOV terms through adaptive multi-looking.

### Radiometric Terrain Correction Gamma-to-Sigma Factor

`/science/LSAR/GCOV/grids/frequency[A|B]/rtcGammaToSigmaFactor`

The RTC Gamma-to-Sigma factor provides factors to normalize the backscatter normalization convention of the GCOV matrix from gamma0 to sigma0.

## Naming Convention
