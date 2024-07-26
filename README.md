# PHIDO-App

Last updated 2024-07-24

## Purpose

This page provides links to key documents and step-by-step instructions for different tasks required for maintaining the [PHIDO-App-2.1](https://bccdc.shinyapps.io/PHIDO/).
<br><br>


## PHIDO-App - operating procedure 

### Summary

| | PHIDO-App 2.1 |
| :-- | :--  |
| **Description** |​ To provide an interface for users to interactively query data related to weekly disease counts and temporal and cyclical trends |
| **​Frequency** | Review the app weekly every Tuesday by 12:00 pm​  |
| **​Prerequisites** | 1. Basic understanding of PHIDO 2.0 (R) and ```renv``` <br> 2. Access to PHRDW CD Data Mart <br> 3. Login access to Central Analytics Platform (CAP), in order to run R Studio with R4.1.1 on CAP servers |
| ​**Audience** | Users from following mailing lists: <br>- _BCCDC_CDAlerts <br>- _BCCDC_IPVPDS_Imms <br>- _BCCDC_PHR_ALL_STAFF <br>- _BCCDC_CEHO |
| **​Links to Folders** | ```\\srvnetapp02.phsabc.ehcnet.ca\bccdc\Depts\Analytics\DSI\RnD\p06_PHIDO_dashboard\working_version\``` <br> (please see Section A) | 
| | User manual of PHIDO 2.0 in R, prepared by Max Xie et al. ```O:\BCCDC\Groups\Analytics\DSI\RnD\p01_PHIDO_2.0\PHIDO_package``` |
| | Validation data compiled by Max Xie et al. ```O:\BCCDC\Groups\Analytics\DSI\RnD\p01_PHIDO_2.0\PHIDO_Validation``` |
| | Login to [shiny.io](https://www.shinyapps.io/admin/#/dashboard) (use email ```data_analytics@bccdc.ca```; password should have been given to all DAs)|
| ​**Average Time** | 30 minutes​  |

Above table extended from [CD Weekly Alerts Procedure](https://your.healthbc.org/sites/BCCDCsurv/analysts/_layouts/15/start.aspx#/SitePages/CD%20Weekly%20Alerts%20Procedure.aspx).
<br><br>
<hr>

### How-to instructions

- Companion guide: [how-to instructions with screenshots](https://tinyurl.com/phido-dashboard)

<details>
<summary> A. Launching Shiny app on your station</summary>

1. Login to your station 
2. Launch [R Studio 4.1.1 via CAP](launch_r4.1.1_cap.md)
3. Choose "Open Project"
4. Copy-paste below:
    ```
    \\srvnetapp02.phsabc.ehcnet.ca\bccdc\Depts\Analytics\DSI\RnD\p06_PHIDO_dashboard\working_version\
    ```
5. Select ```dashboard.Rproj```
6. Execute below

   ```        
   shiny::runApp( 'app.R' )  
   ```
   Note: enter `y` when prompted about installations

</details>




<details>

<summary> 
B. Run script to prepare PHIDO outputs to be read by the PHIDO-App
</summary>

# Overview

There are parts to this step.
- Part 1 involves creating an updated version of ```data/input_1_case_n_attributes.csv``` in the app project folder.
    - In short, this file consists of latest data extracted from CD Mart (precisely, the latest case counts and other attributes such as date of the case, region of the case, etc.).    
- Part 2 involves running ***PHIDO 2.0 R package*** on these latest case counts to generate ```data/phido_output.RData```, which contains several list data types.
- Part 3 involves creating another dataframe that will be used when populating the map widget. 

## Part 1
1. Launch R Studio via Central Analytics Platform
2. Ensure that you're using R4.1.1
3. In R Studio, choose ```File``` > ```Open project```, copy-paste: 
    ```
    \\srvnetapp02.phsabc.ehcnet.ca\bccdc\Depts\Analytics\DSI\RnD\p11_PHIDO_deploy\
    ```
4. Copy-paste below in the console
    ```source( 'main.R') ```   

    - Upon completion of ```main.R```, the script will generate a new file under the app's folder, i.e.:
        ```\\srvnetapp02.phsabc.ehcnet.ca\bccdc\Depts\Analytics\DSI\RnD\p06_PHIDO_dashboard\data\input_1_case_n_attributes.csv```


## Part 2

1. In R Studio, choose ```File``` > ```Open project```, copy-paste: 
    ```
    \\srvnetapp02.phsabc.ehcnet.ca\bccdc\Depts\Analytics\DSI\RnD\p06_PHIDO_dashboard\
    ```

2. Copy-paste below in the console:
   ```source( 'data_prepare/row_data_with_age_sex.R') ``` 

   - This script will update:
       ```data/input_1_cases_n_attributes.csv```
   
3. Copy-paste below in the console
    ```source( 'data_prepare/create_dataset3_list.R') ```
     
    - This script will update within >20 minutes**:
       ```data/phido_output.RData```

**as tested on 2024-07-22. In a later stage, we will automate this step completely

</details>




<details>

<summary> 
C. Publishing changes to Shiny 
</summary>

1. Repeat steps in Section A to test that the dashboard executes fine locally
2. Upon project owner's approval, run ```deployment/PHIDO_dev001_deploy.R``` to publish your changes to the online app
3. Take a coffee break as the project folder (code and intermediate outputs) would require "large" data transfers and will take >5 minutes.

See [example log showing successful R Studio outputs](example_log.md)
 

</details>

<details>
<summary> Adding users </summary>

1. Update the email list to ensure that retired staff will no longer have access to the app  
2. Update the user list by visiting https://www.shinyapps.io/admin/#/application/12298682/users
  - Email login: data_analytics@bccdc.ca
  - Password: [data analysts been given this info]
  - Application visibiity: ensure it stays in ***private*** mode

3. Click on Users to add email of individual users
  - Make sure one line per email address or the URL link sent will become shared

4. In the message box, please copy-paste below:
    ```
    You were added to a special mailing list for secured access to weekly CD alerts.
    
    To log in, create an account with your institutional email.
    
    To adhere to PHSA privacy policies, keep your credentials private.
    
    Thank you for your cooperation.
    ```
    Note that the length of the message is restricted to length of 250 (characters).

5. If users have trouble signing in, please direct them to these [screenshots](user_notes.md). 

![image](https://github.com/user-attachments/assets/ab13149d-cd24-46e9-af29-5120b4fb68e1)

</details>

<details>
<summary>
Appendices to use when extending your own copy 
</summary>

## [Appendix 1: Understanding the code base for modifications](refine.md)

## Appendix 2: Version control via GitLab 

1. [Install Anaconda](https://healthbc.sharepoint.com/sites/BCCDCDataAnalyticsServicePHSA/SitePages/virtual-environments.aspx)  
    - May wish to review [notes on path](https://healthbc.sharepoint.com/sites/BCCDCDataAnalyticsServicePHSA/SitePages/Python-Infrastructure.aspx)
     
2. Launch Git Bash

3. Create a own copy on your personal drive

    ```
    cd \\PHSAhome2.phsabc.ehcnet.ca\user.name1
    mkdir GitLab
    git clone http://lvmgenodh01.phsabc.ehcnet.ca/bccdc/das/dsi/phido-dash-dev/phido-dashboard.git

    ```

4. Review and replicate an eample workflow.

    <details>
    
    <summary> 
    Add new *how-to-nav_v2.png* figure 
    </summary>

    1. Launch Git Bash and navigate to your repository, e.g.

        ```
        cd GitLab/phido-dashboard
        ```

        Or, if you are working from the subfolder on O: drive:

        ```
        cd //srvnetapp02.phsabc.ehcnet.ca/BCcdc/Depts/Analytics/DSI/RnD/p06_PHIDO_dashboard/
        ```


    1. Update your copy by issuing below
        ```
        git pull
        ```

    2. Create a new branch:
        ```
        git branch refine_how-to-nav_png
        git checkout refine_how-to-nav_png
        ```

    3. Create a new version of the how-to-nav PNG and save it under location ```www/image/how-to-nav_v2.png```

    4. Start tracking the newly created file:
        ```
        git add www/image/how-to-nav_v2.png
        ```

    5. Commit this change along with a concise message and push this change to the remote repository like this:
        ```
        git commit -m "refined how-to-nav legend PNG" 
        git push --set-upstream origin refine_how-to-nav_png
        ```

    6. On the browser, submit a **pull request** so the project owner can approve the request for integrating this change into the remote repo upon their review.

    Example [screenshots](https://docs.google.com/presentation/d/1HoJsx0J9jjHDZVovRDCWPjVyC6yVurn2vqYMx8ytVFU/)

    </details>

</details>
 





<br><br><br><br>




<details>

<summary>Q/A</summary>


## Deployment scheme

- PHIDO 1.0: current pipeline producing power point sent by email
- PHIDO-App-2.0: beta prototype that uses PHIDO 2 with mock data 
- PHIDO-App-2.1: working version with real data from CD mart
- PHIDO-App-3.0: CLHA geography will be provided


## Roll out plan

### Phase I.
- Idea: Run both PHIDO 1.0 and PHIDO-app-2.1 in parallel for 2-3 months 
- Towards automation:
    - Run script 1+2+3 every Sunday 9:30pm (script took 90 minutes to finish - on 2024-07-22 / second paired-rev session MX-LT)
    - Run script 4 every Sunday at 11:30pm

### Phase II. 
- Phase out PHIDO 1.0 after 3 months of automation 

</details>

<br><br>

[![CC BY-NC 4.0][cc-by-nc-shield]][cc-by-nc]

This work is licensed under a
[Creative Commons Attribution-NonCommercial 4.0 International License][cc-by-nc].

[![CC BY-NC 4.0][cc-by-nc-image]][cc-by-nc]

[cc-by-nc]: https://creativecommons.org/licenses/by-nc/4.0/
[cc-by-nc-image]: https://licensebuttons.net/l/by-nc/4.0/88x31.png
[cc-by-nc-shield]: https://img.shields.io/badge/License-CC%20BY--NC%204.0-lightgrey.svg
