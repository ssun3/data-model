---
layout: default
title:  "Styleguide, standards, and conventions"
permalink: guide
nav_order: 2
has_children: true
has_toc: false
---

# {{ page.title }}


## General advices

- For column names, variables and functions we use lower_snake_case;
- For enum values, we also use lower_snake_case (because those values might end up becoming columns during the data analysis);
- For data set names in code and classes we CamelCase; 
- For named constants we ALL_CAPS (e.g., PI, MAX_RADIUS);
- For naming data files and data folders see below. 

Note that in some cases data may be aggregated from multiple different sources, each following their own conventions and it might not always be feasible/practical to harmonize them. More on this later. 

Note also that there are usually higher-level standards regarding the naming and structuring of code depending on the particular tool stack people use to analyze data (for example, for Python, there is PEP-8 and Flake-8, for R there is the tidyverse style). It is generally advised to follow such well-known and widely used standards when applicable.
