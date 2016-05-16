# Migrate XML Plugin
This is a XML Plugin custom module for Drupal 8 Migration.  

## Drupal Module Dependencies
Migrate core
Migrate Tools: https://www.drupal.org/project/migrate_tools

##Source Plugin
This module uses xml_plugin as the source.  

##Process Plugin
This module has three process plugins
1. Image Process Plugin
..*This plugin is used to insert images through the source URL value from the XML

2. Taxonomy Process Plugin
..*This plugin is used to insert taxonomy entity references 

3. Entity Reference Process Plugin
..*This plugin is used to insert content type entity references

##Configuration Form
Drupal 8 migration utilizes the yml file as the configuration file to process migration.  The only file that needs to be adjusted is the configuration file.  Configuration files can be uploaded on Drupal admin page.

1. Configuration/Configuration synchronization/Import tab
2. Choose single item
3. Select Migration
4. Paste in the configuration file

Click on the Export tab to see previous migration configurations.  If you want to override previous configuration, get the uuid from the previous configuration accessed through export tab and include the uuid with the updated configuration file and import it again.

#How to Create the Migration Configuration Form

##Basic XML Migration

1. Start out with the empty configuration form:

![alt text](https://raw.githubusercontent.com/poetic/migrate-xml-plugin/development/README%20Screenshots/ss21.png?token=AL2ATFyrF4G2ymE4R7eNuAIvuKwGf3okks5XQ2bEwA%3D%3D "Logo Title Text 1")

2. 
