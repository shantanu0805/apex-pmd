

# README #

## PMD - Static Code Analysis

PMD will be used in all Salesforce Projects to maintain code quality. As a TA on the project please make sure the below steps are followed -

- Enable Pipelines

- Add Repo Configuration Variables (go to Repository Settings --> Repository Variables)


    | Name  | Value | Description |
	| ------------- | ------------- | ------------- |
    | PMD_ARTIFACT  | true  | Set to **true** to get PMD results in a downloadable csv file under Artifacts tab | 
	| PMD_FORMAT  | text  | If **PMD_ARTIFACT** is not **true** then this format will be used to present results in pipeline logs <br> Check [Report formats](https://pmd.github.io/latest/pmd_userdocs_report_formats.html) for all available PMD format options| 
	| PMD_MINIMUM_PRIORITY  | 5  | Rule priority threshold; Rules with lower priority than configured here won't be used. 1 being highest and 5 being lowest. Check [NeuraFlash - Apex Rule List ](https://bitbucket.org/neuraflash/pmd/src/master/apexRules.xml) for rule wise priority| 
	| SF_APEX_DIR  | force-app/main/default/classes/  | Path to Apex Classes in your project: <br>  - For SFDX projects use force-app/main/default/classes/  <br/>  - For Metadata source proejcts use src/classes| 
	| SF_LWC_DIR  | force-app/main/default/lwc/  |  Path to Apex Classes in your project: <br>  - For SFDX projects use force-app/main/default/lwc/  <br/>  - For Metadata source proejcts use src/lwc | 



### bitbucket-pipelines.yml - 

Use [bitbucket-pipelines.yml](https://bitbucket.org/neuraflash/pmd-playground/src/master/bitbucket-pipelines.yml "bitbucket-pipelines.yml") as a reference to default code for PMD steps on your repository. 

Update your bitbucket-pipelines.yml file with the PMD actions defined above. We strongly recommend PMD to be configured to run on every new commit to start. Also, PMD should be used for pull-requests as well.

### Ignoring Files/Components - 

- Add comma separated file paths to [pmdApexIgnoreList.csv](https://bitbucket.org/neuraflash/pmd-playground/src/master/pmdApexIgnoreList.csv "pmdApexIgnoreList.csv") to have PMD ignore select apex classes.

- This file needs to be at the root of your repository similar to bitbucket-pipelines.yml file. 

- Most common use case would be to add existing client files like trigger helpers 

    `force-app/main/default/classes/ITriggerHandler.cls,force-app/main/default/classes/TriggerDispatcher.cls`

- Similarly, we can have [pmdLwcIgnoreList.csv](https://bitbucket.org/neuraflash/pmd-playground/src/master/pmdLwcIgnoreList.csv "pmdLwcIgnoreList.csv") to have PMD ignore select lwc components.

### Notes

- Avoid abuse of ignore lists. PR reviewer should approve the list of ignored files.
- PMD will fail if you are using -ignorelist property but the actual csv file is empty so make sure to update the script to not use -ignorelist accordingly. This is why we have used two separate files so that apex and lwc can be handled separately.

### IDE PMD Plugins
The following are links to IDE plugins to provide developer feedback in the IDE directly (before code commits).  Links to popular ones below.


- [IntelliJ](https://plugins.jetbrains.com/plugin/1137-pmdplugin "IntelliJ")
- [VS Code](https://marketplace.visualstudio.com/items?itemName=chuckjonas.apex-pmd "VS Code")

### Useful Links

- [PMD - Tool Documentation](https://pmd.github.io/latest/index.html)
- [PMD - Default Apex Rules](https://pmd.github.io/latest/pmd_rules_apex.html)
- [NeuraFlash - Apex Rule List ](https://bitbucket.org/neuraflash/pmd/src/master/apexRules.xml)
