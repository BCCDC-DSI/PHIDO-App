# PHIDO-app


# PHIDO dashboard - operating procedure 


## Purpose

- This page provides links to key documents and step-by-step instructions for different tasks required for maintaining the [PHIDO-app-2.0](https://bccdc.shinyapps.io/PHIDO/).
 
| |  CD weekly alerts | PHIDO-app 2.0 |
| :-- | :--  | :-- |
| **Description** |​ To detect an unusual rise in weekly disease counts based on their temporal and cyclical trends.​ | To enable interactive explorations of alerts (sort, etc.) |
| **​Frequency** | Weekly every Tuesday by 1:00 pm​   | NA/ |
| **​Prerequisites** | 1. PHIDO 2.0 (R) <br> 2. Access to PHRDW CD Data Mart | Same |
| ​**Report To** | Users from  <br>- _BCCDC_CDAlerts <br>- _BCCDC_IPVPDS_Imms <br>- _BCCDC_PHR_ALL_STAFF <br>- _BCCDC_CEHO |
| **Rolling Reports** | bcc to _BCCDC_RollingReports | Same |
| **​Links to Folders** | - \\phsabc\root\BCCDC\Groups\Data_Surveillance\PHRDW\CD\Alerts\csv_output <br>- \\phsabc.ehcnet.ca\root\BCCDC\Groups\Analytics\Data_Analysts\Reports_Scripts\Reporting\CD-Alerts-Extract <br>- https://bi.phsa.ca/BCCDC/Reports/CD/Case_Count_Reports  <br>- \\phsabc.ehcnet.ca\root\BCCDC\Groups\CDIS\Epidemiology\epid\CD\1. SURVEILLANCE - General\CD Alert and Rolling reports <br>- \\phsabc\root\BCCDC\Groups\Analytics\Data_Analysts\Reports_Scripts\Reporting\CD-Alerts\Outputs  |  <br> User manual of PHIDO 2.0 prepared by Max ```O:\BCCDC\Groups\Analytics\DSI\RnD\p01_PHIDO_2.0\PHIDO_package``` <br> Validation compiled by Max et al. ```O:\BCCDC\Groups\Analytics\DSI\RnD\p01_PHIDO_2.0\PHIDO_Validation``` <br> [Shiny Login](https://www.shinyapps.io/admin/#/dashboard), use login ```data_analytics```|
| ​**Average Time** | 30 minutes​  | 10 minutes |

Above table extended from [CD Weekly Alerts Procedure](https://your.healthbc.org/sites/BCCDCsurv/analysts/_layouts/15/start.aspx#/SitePages/CD%20Weekly%20Alerts%20Procedure.aspx).

<hr>

### How-to

<details>
<summary> A. Launching dashboard on your station locally
</summary>

1. Login to your station 
2. Launch [R Studio 4.1.1 via CAP](launch_r4.1.1_cap.md)
3. Choose "Open Project"
4. Copy-paste below:
    ```
    \\srvnetapp02.phsabc.ehcnet.ca\bccdc\Depts\Analytics\DSI\RnD\p06_PHIDO_dashboard\beta_version\
    ```
5. Select ```dashboard.Rproj```
6. Execute below and enter `y` when prompted about installations

    ```        
    shiny::runApp( 'app.R' )  
    ```

</details>




<details>

<summary> 
B. Publishing changes to Shiny 
</summary>

1. Repeat steps in Section A to test that the dashboard executes fine locally
2. Upon project owner's approval, run ```deployment/PHIDO_dev001_deploy.R``` to publish your changes to the online app
3. Take a coffee break as the project folder (code and intermediate outputs) would require "large" data transfers and will take >5 minutes.

See [example log showing successful R Studio outputs](example_log.md)
 

</details>

<details>
<summary> Adding users </summary>

- Login under data_analytics@bccdc.ca
- Password: [data analysts been given this info]

</details>

<details>
<summary>
Appendix 1. Extending your own copy 
</summary>

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
    Add new ```how-to-nav_v2.png``` figure 
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





### Misc


<details>

<summary>Q/A</summary>


## Deployment scheme

- PHIDO 1.0: current pipeline producing power point sent by email
- PHIDO-app-2.0: beta prototype, i.e. mock data
- PHIDO-app-2.1: uses real data from CD mart
- PHIDO-app-3.0: CLHA geography will be provided

## Ideas
- Run both PHIDO 1.0 and PHIDO-app-2.1 in parallel for 2-3 months 

</details>




