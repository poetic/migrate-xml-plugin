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
   *This plugin is used to insert images through the source URL value from the XML

2. Taxonomy Process Plugin
   *This plugin is used to insert taxonomy entity references 

3. Entity Reference Process Plugin
   *This plugin is used to insert content type entity references

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

   ![alt text](https://raw.githubusercontent.com/poetic/migrate-xml-plugin/development/README%20Screenshots/ss21.png?token=AL2ATFyrF4G2ymE4R7eNuAIvuKwGf3okks5XQ2bEwA%3D%3D "")

2. Create the name for this migration and place it in id and migration_name.  They need to IDENTICAL. We will use superhero for this example
3. Lable is optional description.  We will use 'Import Superhero Content' for this example.
4. Since we are using the XML Plugin for this migration, insert xml_plugin for source: plugin.
5. Insert the URL path for the XML file for source: path.  We will use this path for this example.
   https://raw.githubusercontent.com/poetic/migrate-xml-plugin/development/custom_migrate/example/super.xml?token=AL2ATB5L8fKnAV_bluTexNyK_JvDUxg9ks5XQ2wlwA%3D%3D
6. base_query is starting query point of the xpath for this migration.  We will use //node for this example.
7. We will cover source: attribute in the later part of the tutorial
8. source: xpath will be used to create a new array for the migration to read
    

