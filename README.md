# NZGOAL Audit Script
Tool for tracking and managing LINZ's obligations under the NZGOAL framework.


## SSP 
LINZ is required to follow the [NZGOAL framework](https://www.ict.govt.nz/guidance-and-resources/open-government/new-zealand-government-open-access-and-licensing-nzgoal-framework/decision-tree/ NZGOAL Data Publishing Frame Work)
for data release and licensing. 

 
We report our compliance with this to the Minister quarterly and we are occasionally audited on how we measure this.

 

## For Data Managers

 
Fill in the [google form](https://docs.google.com/forms/d/e/1FAIpQLSeirs2G_vsjmg4hHymGJDI5axUHuDk9b-0l5GMQtDhuihnVCA/viewform)
, answering the relvant dataset questions. Use your LINZ email address and write the dataset names to be as close as possible to the LDS dataset names. Multiple datasets can be separated by a comma.

Make sure you hit 'save' at the end.

## For LDS Administrators

 
### Managing the Form 

The form can be edited and responses viewed via the land.info.data.service@gmail.com account's Google drive. The password for this account is stored in the Data Services password black book.
 
It is an auditable requirement that prior to publishing all new LDS datasets (see [http://geodeticwiki/LDS_New_Dataset_Process LDS New Dataset Process]) the [https://www.ict.govt.nz/guidance-and-resources/open-government/new-zealand-government-open-access-and-licensing-nzgoal-framework/decision-tree/ NZGOAL Data Publishing Frame Work] must be considered and acted on.

To record the datasets that have undergone the NZGOAL Frame Work Decision Tree process a Google Form has been set up to capture the NZGOAL Decision Tree's responses for each dataset (see above)
 

### Performing the Audit

 

The audit is perform by running a Python script that reads the LDS RSS feed and collects all the LDS ids between user supplied dates (those dates that the user wants to audit to bound). The script then compares these LDS layer ids with the exported Google Form Sheet, first confirming the ids are in the Google Sheet (thus confirming the LDS dataset went through the NZGOAL Framework Decision process) and then groups each layer based on the NZGOAL Questionnaire forms outcomes.

 

To perform the audit the Google Form must be exported as a Tab-separated Values (.tsv) file.

* In the (Google Sheet)[https://docs.google.com/spreadsheets/d/18aSHJg_DM28x6HolaDt25YRxKLSl0hCkPNoxX9hZVyA/edit#gid=1744673523 form responses) select the "Responses" tab
* Open the responses in the Google Sheets by clicking the the green plus button at the top of the responses page.
* Add an ID column as the sheets first column by right clicking column "A" and selecting "insert left". It is IMPORTANT that this column is the first and named "id" for the audit script to run
* The id column must now be populated with each recorded datasets LDS layer id.
 * This is a manual process that involves searching the data sets name (that in the data set name column of the sheet) in the [http://.data.linz.govt.nz LDS] and adding the LDS id to the sheets id column.
 * Multiple layer IDs for a dataset may be comma seperated
* Once all the ids are populated in the Google Sheet - Export the sheet as .tsv. File > Download as > .tsv


Now that the Google sheet has been exported, pull the audit script from the git repo https://github.com/SPlanzer/nzgoal_audit_script. This script reads the RSS feed, gets the Id for every LDS layer/table published between the user supplied dates and ensures that the IDs are in the Google Sheet (exported as .tsv). Once it has done this it will output the results in four categories. 

* Publish: the LDS Id was found in the sheet and the NZGOAL based form confirmed the data manager was OK to publish 
* Publish with restrictions: the LDS Id was found in the sheet and the NZGOAL based form confirmed the data manager was OK to publish but with restrictions
* Do Not Publish: the LDS Id was found in the sheet and the NZGOAL based form indicated the data manager shall not published the dataset (This category should never find a result as it indicates the Data Manager published against the NZGoal advice)
* No Id in Sheet: The LDS layer id was not found in the sheet. This suggests to the auditor that the layer was published but did not go through the NZGOAL decision tree for data publishing.   

 
In the terminal run the below. The script will prompt the user dates and path to .tsv

   '''python <path to script>/nzgoal_audit.py''' 

  

The script takes three user inputs. 
* date_from: only consider LDS layers published after this date
* date_to: only consider LDS layers published prior to this date
* tsv path: full directory path to the Google Form exported tsv.

### Saving the results

On the final run and report for every quarter, save the files below to Objective (https://linzone/id:fA268176) in case we get externally audited about this.

Need to save:

* Copy of script code
* Input (TSV export, see above)
* Log of script results

''''python <path to script>/nzgoal_audit.py > Q4_results.txt'''
