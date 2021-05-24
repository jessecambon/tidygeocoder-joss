---
title: 'tidygeocoder: An R package for geocoding'
tags:
  - R
  - geocoding
authors:
  - name: Jesse Cambon
    orcid: 0000-0001-6854-1514
    affiliation: 1
  - name: Diego Hernangómez
    orcid: 0000-0001-8457-4658
    affiliation: 1
  - name: Christopher Belanger
  - orcid: 0000-0003-2070-5721
    affiliation: 1
affiliations:
 - name: Independent Researcher
   index: 1
date: 15 May 2021
bibliography: paper.bib

---

# Summary

Tidygeocoder is an R package that provides an intuitive uniform interface for users of the R programming language [@R:2021] to easily incorporate data from geocoding services into their projects. Geocoding (also called "forward geocoding") is the process of obtaining geographic coordinates (longitude and latitude) from an address or a place name, and "reverse geocoding" is the process of obtaining an address or place name from geographic coordinates. Many geocoding services are accessible as web services via an API, and to leverage these services users must execute API queries and then extract and format the data received from the service as necessary. However, geocoder services vary widely in their API interfaces, capabilities, and output data formats, which makes it difficult for users to adopt a new service or switch between them. Tidygeocoder addresses this gap by providing users with a simple and consistent interface to a number of popular geocoding services, so that users can spend less time worrying about API parameters and more time developing their analyses.

# Motivation

The R programming language [@R:2021] is commonly used for geospatial data analysis and manipulation. To use a geocoder service, R users must execute an API query and then format the data they receive back from the service and incorporate it into their project. Geocoder services vary widely in their API parameters, capabilities, and output data formats, so this process can be complex and require a variety of approaches. This lack of consistency can present major difficulties for users and is the motivation for the tidygeocoder package.

For example, the same service can require a different query and return output data in a different format depending on whether single input geocoding or batch geocoding is used. For example, the Nominatim service has separate city, state, country, postal code, and county parameters that can be used to specify components of an address. Other services such as Google only use a single address parameter to construct queries. Additionally, the parameter names are not standardized between services. The single address parameter for Nominatim is `“q”` (for query) while for Google it is named `“address”`. Other services such MapBox and TomTom use a non-standard query string format for their queries. 

Additionally, for reverse geocoding, some services such as Nominatim use separate latitude and longitude parameters whereas other services combine latitude and longitude into a single input parameter. Services can also require other parameters such as API keys and the desired output data format.

Working with data from geocoding services can also require a variety of different data manipulation operations. Services often return nested JSON data, but there is no standard format for this data so users must locate the relevant data they wish to extract and format it as needed. Output data formats can also vary even when using the same service depending on whether single input or batch geocoding was used.

# Functionality

The tidygeocoder package was created to minimize the amount of effort required to use geocoder services in an R workflow. Additionally, the package is structured to make adding and maintaining support for geocoder services a modular and streamlined process. The package provides users a mechanism to access geocoder services through a unified interface and to receive output data in a tidy dataframe format [@Wickham:2014]. A universal set of input parameters is mapped to the specific API parameters for each service and the relevant parts of the output data are extracted and formatted. This reduces the amount of time and effort required utilize geocoder services and provides the ability to seamlessly transition between services.

The package also provides a variety of convenience functionality to simplify the geocoding process. The package automatically adjusts the rate of querying based on the geocoder service selected to comply with usage restrictions. All inputs to geocoder services are deduplicated before geocoder queries are constructed to avoid redundant or needlessly large queries. The httr package [@httr] is used to execute API queries, the jsonlite package [@jsonlite] is used to convert the JSON data returned from geocoder services into dataframes, and the tibble [@tibble] and dplyr [@dplyr] packages provide tidy dataframe and data manipulation functionality [@Wickham:2019].

Built-in dataframes are used to store important information on geocoder services such as parameter names, the maximum query rate, and the maximum allowed size of batch queries. This makes these values transparent to users and allows developers to easily add and edit these values as needed. Some package documentation is directly generated from these dataframes to reduce the need for the manual updating of documentation.

# Acknowledgements

We acknowledge contributions from .........

# References