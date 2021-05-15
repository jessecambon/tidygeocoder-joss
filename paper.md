---
title: 'tidygeocoder: An R package for geocoding'
tags:
  - rstats
  - geocoding
authors:
  - name: Jesse Cambon
    orcid: 0000-0001-6854-1514
  - name: Diego Hernangómez
    orcid: 0000-0001-8457-4658
date: 15 May 2021
bibliography: paper.bib

---

# Summary

Geocoding is the process of obtaining geographic coordinates (longitude and latitude) from an address or a place name. Geocoding is also referred to as forward geocoding to distinguish it from reverse geocoding which is the process of obtaining an address or place name from geographic coordinates. Both forward and reverse geocoding can be performed by geocoding services, which are web services that are accessible via an API. Either one input (an address or geographic coordinate) can be submitted per query, which we will refer to as single input geocoding, or multiple inputs can be submitted per query in what is known as batch geocoding. In addition to geographic coordinates, addresses, and place names, geocoder services can offer a wide variety of other data such as US Census geographies and stadium capacities.

Geocoding services are an important data source for analysts, researchers, and developers who work with geospatial data and there are many such services available. These services can vary widely in their API interfaces, capabilities, and output data formats. Tidygeocoder is an R package that provides an intuitive uniform interface for users of the R programming language **(<insert reference>)** to easily incorporate data from geocoding services into their projects.

# Motivation

The R programming language **(<insert reference here>)** is commonly used for geospatial data analysis and manipulation **(sf, tidycensus, dplyr, …)**. To make use of a geocoder service, R users must execute an API query and then format the data they receive back from the service and incorporate it into their project. This process can require a variety of approaches since geocoder services vary widely in their API parameters, capabilities, and output data formats. Additionally the same service can require a different query and return output data in a different format depending on whether single input geocoding or batch geocoding is used. These discrepancies 

For example, the Nominatim service has separate city, state, country, postal code, and county parameters that can be used to specify components of an address. Other services such as Google only use a single address parameter to construct queries. Additionally, the parameter names are not standardized between services. The single address parameter for Nominatim is `“q”` (for query) while for Google it is named `“address”`. Other services such MapBox and TomTom use a non-standard query string format for their queries.
Additionally, for reverse geocoding, some services such as Nominatim use separate latitude and longitude parameters whereas other services combine latitude and longitude into a single input parameter.

Working with the data from the geocoding service can also require a variety of different data manipulation operations. Services often return nested JSON data, but there is no standard format for this data so users must locate the data they wish to extract and format it as needed. Output data formats can also vary even when using the same service depending on whether single input or batch geocoding was used.

# Functionality

The tidygeocoder package was created to minimize the amount of effort required to use geocoder services in an analytics workflow. Additionally, the package is structured to make adding and maintaining support for geocoder services a modular and streamlined process. With tidygeocoder, users can access geocoder services through a unified interface and receive output data in a tidy dataframe format **(<insert tidy data reference>)**. The httr package **(<insert reference>)** is used to execute API queries, the jsonlite package **(<insert reference>)** is used to parse output data from geocoder services, the tibble package **(<insert reference>)** provides a dataframe format, and the dplyr package **(<insert reference>)** is used for data manipulation.

This reduces the amount of time required to create API queries and to parse the output returned from the geocoder service. Built-in dataframes are used to store important information on geocoder services such as parameter names, the maximum query rate, and the maximum allowed size of batch queries. This makes these values transparent to users and allows developers to easily add and edit these values as needed. Some package documentation is directly generated from these dataframes to reduce the need for the manual updating of documentation. For single input forward geocoding, a single dataframe maps universal parameter names to the specific API parameter names for each service, allowing the same functions to be used to create and execute queries for all supported geocoding services. The package also automatically adjusts the rate of querying based on the geocoder service selected to comply with usage restrictions.

# Statement of need

`Gala` is an Astropy-affiliated Python package for galactic dynamics. Python
enables wrapping low-level languages (e.g., C) for speed without losing
flexibility or ease-of-use in the user-interface. The API for `Gala` was
designed to provide a class-based and user-friendly interface to fast (C or
Cython-optimized) implementations of common operations such as gravitational
potential and force evaluation, orbit integration, dynamical transformations,
and chaos indicators for nonlinear dynamics. `Gala` also relies heavily on and
interfaces well with the implementations of physical units and astronomical
coordinate systems in the `Astropy` package [@astropy] (`astropy.units` and
`astropy.coordinates`).

`Gala` was designed to be used by both astronomical researchers and by
students in courses on gravitational dynamics or astronomy. It has already been
used in a number of scientific publications [@Pearson:2017] and has also been
used in graduate courses on Galactic dynamics to, e.g., provide interactive
visualizations of textbook material [@Binney:2008]. The combination of speed,
design, and support for Astropy functionality in `Gala` will enable exciting
scientific explorations of forthcoming data releases from the *Gaia* mission
[@gaia] by students and experts alike.

# Mathematics

Single dollars ($) are required for inline mathematics e.g. $f(x) = e^{\pi/x}$

Double dollars make self-standing equations:

$$\Theta(x) = \left\{\begin{array}{l}
0\textrm{ if } x < 0\cr
1\textrm{ else}
\end{array}\right.$$

You can also use plain \LaTeX for equations
\begin{equation}\label{eq:fourier}
\hat f(\omega) = \int_{-\infty}^{\infty} f(x) e^{i\omega x} dx
\end{equation}
and refer to \autoref{eq:fourier} from text.

# Citations

Citations to entries in paper.bib should be in
[rMarkdown](http://rmarkdown.rstudio.com/authoring_bibliographies_and_citations.html)
format.

If you want to cite a software repository URL (e.g. something on GitHub without a preferred
citation) then you can do it with the example BibTeX entry below for @fidgit.

For a quick reference, the following citation commands can be used:
- `@author:2001`  ->  "Author et al. (2001)"
- `[@author:2001]` -> "(Author et al., 2001)"
- `[@author1:2001; @author2:2001]` -> "(Author1 et al., 2001; Author2 et al., 2002)"

# Figures

Figures can be included like this:
![Caption for example figure.\label{fig:example}](figure.png)
and referenced from text using \autoref{fig:example}.

Figure sizes can be customized by adding an optional second parameter:
![Caption for example figure.](figure.png){ width=20% }

# Acknowledgements

We acknowledge contributions from _________________

# References