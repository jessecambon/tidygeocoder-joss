---
title: 'tidygeocoder: An R package for geocoding'
tags:
  - rstats
  - geocoding
authors:
  - name: Jesse Cambon
    orcid: 0000-0001-6854-1514
    affiliation: 1
  - name: Diego Hernangómez
    orcid: 0000-0001-8457-4658
    affiliation: 1
affiliations:
 - name: Independent Researcher
   index: 1
date: 15 May 2021
bibliography: paper.bib

---

# Summary

Geocoding is the process of obtaining geographic coordinates (longitude and latitude) from an address or a place name. Geocoding is also referred to as forward geocoding to distinguish it from reverse geocoding which is the process of obtaining an address or place name from geographic coordinates. Both forward and reverse geocoding can be performed by geocoding services, which are web services that are accessible via an API. Either one input (an address or geographic coordinate) can be submitted per query, which we will refer to as single input geocoding, or multiple inputs can be submitted per query in what is known as batch geocoding. In addition to geographic coordinates, addresses, and place names, geocoder services can offer a wide variety of other data such as US Census geographies and stadium capacities.

Geocoding services are an important data source for analysts, researchers, and developers who work with geospatial data and there are many such services available. These services can vary widely in their API interfaces, capabilities, and output data formats. Tidygeocoder is an R package that provides an intuitive uniform interface for users of the R programming language [@R:2021] to easily incorporate data from geocoding services into their projects.

# Motivation

The R programming language [@R:2021] is commonly used for geospatial data analysis and manipulation. To make use of a geocoder service, R users must execute an API query and then format the data they receive back from the service and incorporate it into their project. This process can require a variety of approaches since geocoder services vary widely in their API parameters, capabilities, and output data formats. Additionally the same service can require a different query and return output data in a different format depending on whether single input geocoding or batch geocoding is used. These discrepancies 

For example, the Nominatim service has separate city, state, country, postal code, and county parameters that can be used to specify components of an address. Other services such as Google only use a single address parameter to construct queries. Additionally, the parameter names are not standardized between services. The single address parameter for Nominatim is `“q”` (for query) while for Google it is named `“address”`. Other services such MapBox and TomTom use a non-standard query string format for their queries.
Additionally, for reverse geocoding, some services such as Nominatim use separate latitude and longitude parameters whereas other services combine latitude and longitude into a single input parameter.

Working with the data from the geocoding service can also require a variety of different data manipulation operations. Services often return nested JSON data, but there is no standard format for this data so users must locate the data they wish to extract and format it as needed. Output data formats can also vary even when using the same service depending on whether single input or batch geocoding was used.

# Functionality

The tidygeocoder package was created to minimize the amount of effort required to use geocoder services in an analytics workflow. Additionally, the package is structured to make adding and maintaining support for geocoder services a modular and streamlined process. With tidygeocoder, users can access geocoder services through a unified interface and receive output data in a tidy dataframe format [@Wickham:2014]. The httr package [@httr] is used to execute API queries, the jsonlite package [@jsonlite] is used to parse output data from geocoder services, the tibble package [@tibble] provides a dataframe format, and the dplyr package [@dplyr] is used for data manipulation.

This reduces the amount of time required to create API queries and to parse the output returned from the geocoder service. Built-in dataframes are used to store important information on geocoder services such as parameter names, the maximum query rate, and the maximum allowed size of batch queries. This makes these values transparent to users and allows developers to easily add and edit these values as needed. Some package documentation is directly generated from these dataframes to reduce the need for the manual updating of documentation. For single input forward geocoding, a single dataframe maps universal parameter names to the specific API parameter names for each service, allowing the same functions to be used to create and execute queries for all supported geocoding services. The package also automatically adjusts the rate of querying based on the geocoder service selected to comply with usage restrictions.

# Statement of need

# Acknowledgements

We acknowledge contributions from _________________

# References