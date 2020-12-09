+++
title = "A CEEMID első regionális szintű open data adatpublikációja"

date = 2020-04-16T17:00:00
lastmod = 2020-04-16T17:30:00
draft = false

authors = ["Daniel Antal, CFA"]

tags = ["CEEMID", "open-data", "music-demand", "European Music Observatory"]

projects = ["CEEMID", "opendata"]

summary = "Annak előkészületeként, hogy a CEEMID nyílt forráskodú adatintegrációs rendszerként és adatforrásként a European Music Observatory egyik alapja lehessen, megkezdtük a regionális (országhatárokon belüli) adatszolgáltatást."

# Featured image
[image]
  # Caption (optional)
  caption = "Six years of regional data visualized"

  # Focal point (optional)
  # Options: Smart, Center, TopLeft, Top, TopRight, Left, Right, BottomLeft, Bottom, BottomRight
  focal_point = "Center"

  # Show image only in page previews?
  preview_only = false
  
[[gallery_item]]
album = "gallery"
image = "ceemid_regional_social_media_use_2011.jpg"
caption = "Internet use: participating in social networks (2011)"

[[gallery_item]]
album = "gallery"
image = "ceemid_regional_social_media_use_2015.jpg"
caption = "Internet use: participating in social networks (2015)"

[[gallery_item]]
album = "gallery"
image = "ceemid_regional_social_media_use_2019.jpg"
caption = "Internet use: participating in social networks (2019)"

[[gallery_item]]
album = "gallery"
image = "metadata_ceemid_regional_social_media_use_2011.jpg"
caption = "CEEMID metadata summary (2011)"

[[gallery_item]]
album = "gallery"
image = "metadata_ceemid_regional_social_media_use_2015.jpg"
caption = "CEEMID metadata summary (2015)"

[[gallery_item]]
album = "gallery"
image = "metadata_ceemid_regional_social_media_use_2019.jpg"
caption = "CEEMID metadata summary (2019)"

+++

_Internet use: participating in social networks (creating user profile, posting messages or other contributions to facebook, twitter, etc.) [percentage of individuals]_ shows the development of social media use in the past 10 years in very high detail.  Social media is one of the most important ways to communicate with fans and find audiences for gigs, performances and to share new releases.

![Social media use 2011-2019](/img/dataanimation/internet_use_social_networks.gif)

The chosen dataset is highlighting several new priorities of CEEMID.  This indicator, which is based on a [Eurostat statistical product](https://appsso.eurostat.ec.europa.eu/nui/show.do?dataset=isoc_r_iuse_i&lang=en), has a much higher data quality than the Eurostat release, it is easier to use, and goes beyond the detail of national statistics.  It contains data on 411 territories in Europe, including countries, provinces and smaller regions, even some metropolitan areas.

The dataset is available on the European open research data repository, [Zenodo](https://zenodo.org/record/3754574#.XpimX8gzbIU). It will be updated annually. [![DOI](https://zenodo.org/badge/DOI/10.5281/zenodo.3754574.svg)](https://doi.org/10.5281/zenodo.3754574) 

The processing information is available in the dataset.  First, the CEEMID open source software corrects the regional boundaries when changes affected them in the past decade (_see [Programatic Approach To Work With European Regional Data Panels](/post/2020-02-13-regional_eurostat/)_).

When data was missing in the end of the dataset, the last observation is carried forward, when in the beginning, the next observation is carried backwards.  Gaps in the data are interpolated using linear interpolation. Whenever data was available on a larger (provincial level), we imputed it to the smaller regional units. In the next release, panel and time series model based forecasts will be included, too. 

The data contains both current NUTS2016 standard national/regional references, and the NUTS2013 standard for backward compatibility. Further documentation will be available on our methodology on the [documentation.ceemid.eu](https://documentation.ceemid.eu) wiki website.

At last, the data was put into a table that complies with the [tidy data](https://www.jstatsoft.org/article/view/v059i10) principles for easier processing on computers and immediate use in spreadsheet applications. 

_Use this in your article? Further research? Collaboration? Let's get in touch on [LinkedIn](https://www.linkedin.com/in/antaldaniel/), [Twitter](https://twitter.com/antaldaniel), or via [danielantal.eu](https://danielantal.eu/#contact)_


{{< gallery >}} 

