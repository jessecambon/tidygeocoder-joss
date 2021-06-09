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
    orcid: 0000-0003-2070-5721
    affiliation: 1
  - name: Daniel Possenriede
    orcid: 0000-0002-6738-9845
    affiliation: 1
affiliations:
 - name: Independent Researcher
   index: 1
date: 15 May 2021
bibliography: paper.bib
---

# Summary

Tidygeocoder [@tidygeocoder:2021] is a package for the R programming language [@R:2021] that provides an intuitive uniform interface for researchers and analysts to perform geocoding. Geocoding (also called "forward geocoding") is the process of obtaining geographic coordinates (longitude and latitude) from an address or a place name, while reverse geocoding is the process of obtaining an address or place name from geographic coordinates. Forward and reverse geocoding play an important role in geospatial data analysis and are commonly performed through the use of web-based geocoding services [@Kounadi:2013; Kilic:2020].

To use geocoding services users must execute an API query and then extract and format the data received from the service as necessary for their use case. However, geocoder services vary widely in their API parameters, capabilities, and output data formats, which can make it difficult for users to adopt a new service or switch between them. Tidygeocoder addresses this challenge by providing users with a simple and consistent interface to a number of popular geocoding services, so that users can spend less time worrying about data manipulation and API parameters and more time developing their analyses. Tidygeocoder has been used and cited by researchers for a number of academic publications [@Walming:2021; @Raymond:2021; @King:2020; @Decaire:2020].

# Motivation

The R programming language [@R:2021] is commonly used for geospatial data analysis and research. To use a geocoder service, R users must execute an API query, extract the relevant data received from the service, and then perform the data manipulations required to incorporate this data into their project. Geocoder services vary widely in their API parameters, capabilities, and output data formats, so this process can be complex and require a variety of approaches. This lack of consistency can present major difficulties for users and is the motivation for the tidygeocoder package.

For an example of how parameters can vary between APIs, the Nominatim service has separate city, state, country, postal code, and county parameters that can be used to specify components of an address. Other services such as Google only use a single address parameter to construct queries. Additionally, the parameter names are not standardized between services. The single address parameter for Nominatim is `“q”` (for query) while for Google it is named `“address”`. Other services such MapBox and TomTom use a non-standard query string format for their queries. Also, the same service can require a different API query and return output data in a different format depending on whether one input is given ("single input geocoding") or multiple inputs are given ("batch geocoding"). 

For reverse geocoding, some services such as Nominatim use separate latitude and longitude parameters, whereas other services combine latitude and longitude into a single input parameter. Services can also require other parameters such as API keys and the desired output data format.

Working with data from geocoding services can also require a variety of data manipulation. Services often return nested JSON data, but there is no standard format for this data so users must locate the relevant data they wish to extract and format it as needed. Output data formats can also vary even when using the same service depending on whether single input or batch geocoding was used.

As a result of this complexity it can be difficult to get one geocoding service to work properly, let alone more than one. Since geocoding services are an important source of geospatial data for analysts, researchers, and developers, tidygeocoder's intuitive uniform interface to multiple geocoding services is an important contribution to the field.

# Functionality

The tidygeocoder package was created to minimize the amount of effort required to use geocoder services in an R workflow. Additionally, the package is structured to make adding and maintaining support for geocoder services a modular and streamlined process. The package provides users a mechanism to access geocoder services through a unified interface and to receive output data in a tidy dataframe format [@Wickham:2014]. A universal set of input parameters is mapped to the specific API parameters for each service and the relevant parts of the output data are extracted and formatted. This reduces the amount of time and effort required utilize geocoder services and provides the ability to seamlessly transition between services. 

For forward geocoding, users can provide addresses and place names using either a single parameter or multiple address component parameters (ie. city, state, country, etc.). For reverse geocoding, the latitude and longitude parameters are specified with two separate parameters. These inputs can be provided standalone (ie. a single value or vector) or within a dataframe.

Tidygeocoder sets the rate of querying automatically based on the usage policy restrictions of the selected geocoder service. All inputs to geocoder services are deduplicated before geocoder queries are constructed to avoid redundant or needlessly large queries. Built-in dataframes are used to store important information on geocoder services such as parameter names, the maximum query rate, and the maximum allowed size of batch queries. This makes these values transparent to users and allows developers to easily add and edit these values as needed. Some package documentation is directly generated from these dataframes to reduce the need for the manual updating of documentation.

The httr package [@httr] is used to execute API queries, the jsonlite package [@jsonlite] is used to convert the JSON data returned from geocoder services into dataframes, and the tibble [@tibble] and dplyr [@dplyr] packages provide data manipulation and a tidy dataframe format [@Wickham:2019].

# References
