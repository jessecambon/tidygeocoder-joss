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

Tidygeocoder [@tidygeocoder:2021] is a package for the R programming language [@R:2021] that provides an intuitive uniform interface for researchers and analysts to perform geocoding. Geocoding (also called "forward geocoding") is the process of obtaining geographic coordinates (longitude and latitude) from an address or a place name, while reverse geocoding is the process of obtaining an address or place name from geographic coordinates. Forward and reverse geocoding play an important role in geospatial data analysis and are commonly performed through the use of web-based geocoding services [@Kounadi:2013; @Kilic:2020].

To use a geocoding service you must execute an API query and then extract and format the data received from the service and incorporate it into your project. However, geocoding services vary widely in their API parameters, capabilities, and output data formats, which can make it difficult for users to adopt a new service or switch between them. Tidygeocoder addresses this challenge by providing users with a simple and consistent interface to a number of popular geocoding services, so that users can spend less time worrying about data manipulation and API parameters and more time developing their projects. Tidygeocoder is actively used and cited in academic research and publications [@Hegde:2021; @Walming:2021; @Raymond:2021; @King:2020; @Decaire:2020].

# Challenges in Geocoding

Tidygeocoder was created to address obstacles that can make geocoding time-consuming and challenging. The first challenge in geocoding is to construct an API query to a geocoding service. However, the APIs of geocoding services differ greatly. For instance, the Nominatim service, which is based on OpenStreetMap data [@OSM:2017], has separate city, state, country, postal code, and county parameters that can be used to specify components of an address. Other services such as Google only use a single address parameter to construct queries. 

Additionally, the parameter names are not standardized between services. The single address parameter for Nominatim is `“q”` (for query) while for Google it is named `“address”`. Some services such MapBox and TomTom use a non-standard query string format, which requires a different approach to constructing a query. Also, the same service can require a different API query and return output data in a different format depending on whether one input is given ("single input geocoding") or multiple inputs are given ("batch geocoding"). 

For reverse geocoding, some services such as Nominatim use separate latitude and longitude parameters, whereas other services combine latitude and longitude into a single input parameter. Services can also require other parameters such as an API key and the desired output data format (ie. "json"). Working with data from geocoding services can also require a variety of data manipulation work. Services often return nested JSON data, but there is no standard format for this data so users must locate the relevant data they wish to extract and format it as needed. Output data formats can also vary even when using the same service depending on whether single input or batch geocoding was used.

# Functionality

The tidygeocoder package provides users a mechanism to access geocoding services through a unified interface and receive output data in a tidy dataframe format [@Wickham:2014] that can be easily incorporated into projects. A universal set of input parameters is mapped to the specific API parameters for each service and the relevant parts of the output data are extracted and formatted. This reduces the amount of time and effort required to utilize geocoding services and provides the ability to seamlessly transition between services. 

For forward geocoding, users can provide addresses and place names using either a single parameter or multiple address component parameters (ie. city, state, country, etc.). For reverse geocoding, the latitude and longitude parameters are specified with two separate parameters. These inputs can be provided standalone (ie. a single value or vector) or within a dataframe.

Tidygeocoder sets the rate of querying automatically based on the usage policy restrictions of the selected geocoding service. Only unique inputs are sent to geocoding services even if duplicate data is provided to avoid redundant or needlessly large queries. Built-in dataframes are used to store important information on geocoding services such as parameter names, the maximum query rate, and the maximum allowed size of batch queries. This makes these values transparent to users and allows developers to easily modify these values as needed. Some package documentation is directly generated from these dataframes to reduce the need for manual updates.

The httr package [@httr] is used to execute API queries, the jsonlite package [@jsonlite] is used to convert JSON data returned from geocoding services into dataframes, the dplyr [@dplyr] package is used for data manipulation, and the tibble [@tibble] package provides a tidy dataframe format [@Wickham:2019].

# References
