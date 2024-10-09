
![image](https://github.com/user-attachments/assets/146ba070-048d-442a-b5dd-f5c2cf5768f3)


PHIDO is a statistical algorithm that determines whether a sequence of weekly case counts is unusual compared to any trends shown over the previous years. More specifically, it estimates the expected value ("expected count") for each epi-week based on counts from the previous epi-weeks from the past five years. When an expected count disagrees with the actual value ("observed count") substantially in a statistical sense, an alert is generated. Different thresholds may be set for different diseases; users may interact with the menu to explore the effects of the threshold. Note that rare diseases will always lead to an alert. 

In spring of 2024, [PHIDO-App](https://bccdc.shinyapps.io/PHIDO/) was implemented with R Shiny that would allow users to interactively understand the alerts generated by the PHIDO algorithm, e.g. functions:
- To explore counts and alerts by geography
- To examine the trendtimes for a particular disease-region combination
- To aggregate analysis data based on gender
- ...  


## Purpose of this repo

This repo provides links to key documents and step-by-step instructions for different tasks required for maintaining the [PHIDO-App](https://bccdc.shinyapps.io/PHIDO/).


<br>


## Diseases reflected by the app

[List of common diseases](metadata/CD_by_prescribed_agents.md)

<details>
  
<summary>List of rare diseases</summary>

```
Anthrax
Botulism
Brucella Infection
Chlamydia (neonatal)
Congenital Rubella Syndrome
Creutzfeldt-Jakob Disease: Classic/Unspecified
Creutzfeldt-Jakob Disease: Variant
Crimean Congo Fever
Cyclospora Infection
Diphtheria: Carrier
Diphtheria: Case
Ebola
Gonorrhea (neonatal)
Haemophilus Influenzae (invasive type b)
Hantavirus Infection
Hepatitis B: Acute
Hepatitis D
Hepatitis E
Herpes (congenital)
Human Immunodeficiency Virus (HIV) Infection (congenital/neonatal)
Lassa Fever
Legionella Infection
Listeria Infection (invasive)
Marburg Fever
Measles
Meningococcal Disease (invasive)
Middle East Respiratory Syndrome Coronavirus (MERS-CoV)
Mpox
Plague
Poliomyelitis
Q fever
Rabies
Rubella (non-congenital)
Subacute Sclerosing Panencephalitis
Syphilis (congenital)
Tetanus
Toxoplasma Infection
Tularemia Infection
Varicella (congenital)
Viral Hemorrhagic Fever: Other
West Nile Virus
Yellow Fever
``` 
</details>





## Important links

### Maintaining the app

- [Standard Operating Procedure](sop.md) for use by data analysts

### More data?

Below are links to the diseases not currently reported on the PHIDO-App:

- Weekly PDF reports [report latest data on SARS-CoV-2, RSV, ERV, influenza](http://www.bccdc.ca/Health-Info-Site/Documents/Respiratory_data/respiratory_surveillance_2024-10-03.pdf)
- [Shellfish harvesting status map](http://www.bccdc.ca/health-professionals/professional-resources/shellfish-harvesting-sites-status-map)
- ...
  
### Details on the algorithm

- [PHIDO user manual v2](https://healthbc.sharepoint.com/sites/BCCDCDataAnalyticsServicePHSA/_layouts/15/download.aspx?SourceUrl=/sites/BCCDCDataAnalyticsServicePHSA/Epidemiological%20Methods/PHIDO%20user%20manual%20V2%20for%20sharepoint.pdf)
- [Cliff's technical notes](r_package)


<br>


## Terms

- Case counts: counts of case records pulled from the Panorama system
    - Types: Confirmed, confirmed Epi-Linked, Clinical, Probable (exclude suspected cases)
- Expected count: the count estimated by PHIDO algorithm using time-series of historical counts


<br> 

Revision history
- v1.0, 2024-08-09
- v1.2, 2024-10-07

<br> 

[![CC BY-NC 4.0][cc-by-nc-shield]][cc-by-nc] This work is licensed under a [Creative Commons Attribution-NonCommercial 4.0 International License][cc-by-nc]. [![CC BY-NC 4.0][cc-by-nc-image]][cc-by-nc]

[cc-by-nc]: https://creativecommons.org/licenses/by-nc/4.0/
[cc-by-nc-image]: https://licensebuttons.net/l/by-nc/4.0/88x31.png
[cc-by-nc-shield]: https://img.shields.io/badge/License-CC%20BY--NC%204.0-lightgrey.svg
