# byoa-sample-algorithm

This repository contains a scaffold for the respository structure required for Euro Data Cube - Insights On Demand (aka BYOA Bring Your Own Algorithm) if the algorithm is provided through an [OGC application package](https://docs.ogc.org/bp/20-089r1.html) as defined trough [CWL](https://www.commonwl.org/).

The sample algorithm uses this [sample](https://github.com/EOEPCA/eoepca/blob/9b1ec50965c575c2a9ba8271173fad7d3dee3a91/test/acceptance/02__Processing/01__ADES/data/application-package-cwl.cwl) CWL file to generate the NDVI for S2L2A products as
- transparently resolved via `https://earth-search.aws.element84.com/v1/search?datetime=$time_range&intersects=$aoi&collections=sentinel-2-l2a` (also see parameters below) and
- automatically staged-in (i.e. downloaded and bound)
to the process.

While the [EOEPCA ADES](https://eoepca.github.io/proc-ades/master/) building block is internally used to execute the process as defined through CWL, this [complexity](https://github.com/EOEPCA/eoepca/blob/9b1ec50965c575c2a9ba8271173fad7d3dee3a91/test/acceptance/02__Processing/01__ADES/data/ADES-processing.md) is abstracted away by the BYOA engine.

From provider perspective it is only necessary to 
- bring a [specific](ogc-capp-package.cwl) CWL file to describe the algorithm
- define the resolution strategy via STAC API (e.g. `https://earth-search.aws.element84.com/v1/search`) to get the products automatically staged-in for processing
- come up with a [pricing model](estimate_costs.ipynb) for the offer on EDC marketplace

Please consult the [EDC documentation](https://eurodatacube.com/documentation/offer_algorithms_for_on_demand_data_generation) for more information.

### Parameters

This algorithm can be onboarded to the EDC platform using the following parameter specification:

```javascript
[
  {
    "description": "Area of interest",
    "id": "aoi",
    "name": "Area of interest",
    "optional": false,
    "type": "bbox"
  },
  {
    "description": "Time Range",
    "id": "time_range",
    "name": "Time Range",
    "optional": false,
    "type": "daterange"
  }
]
```

