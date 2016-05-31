# Migrate XML Plugin
This is a XML Plugin custom module for Drupal 8 Migration.  Drupal 8 migration utilizes the yml file as the configuration file to process migration.  The only file that needs to be adjusted is the configuration file.

## Drupal Module Dependencies
Migrate core
Migrate Tools: https://www.drupal.org/project/migrate_tools

##Source Plugin
This module uses xml_plugin as the source.

##Process Plugin
This module has three process plugins:

1. Image Process Plugin
   * This plugin is used to insert images through the source URL value from the XML

2. Taxonomy Process Plugin
   * This plugin is used to insert taxonomy entity references

3. Entity Reference Process Plugin
   * This plugin is used to insert content type entity references

#How to Migrate Using Migrate XML Plugin

##Create Basic Migration Configuration Form

This is the example xml file we will use for this tutorial.  You can find this file in the example folder.

![xml example](https://github.com/poetic/migrate-xml-plugin/blob/development/README%20Screenshots/xml%20screenshot.png)

1. Start out with the empty configuration form:

   ![ss21](https://github.com/poetic/migrate-xml-plugin/blob/development/README%20Screenshots/ss21.png)

2. Create the name for this migration and place it in id and migration_name.  They need to IDENTICAL. We will use superhero for this example
3. Label is optional description.  We will use 'Import Superhero Content' for this example.
4. source: plugin tells migration which source plugin this configuration will use.  Since we are using the XML Plugin for this  migration, insert xml_plugin for source: plugin.
5. Insert the URL path for the XML file for source: path.  We will use this path for this example.
   https://raw.githubusercontent.com/poetic/migrate-xml-plugin/development/custom_migrate/example/super.xml?token=AL2ATB5L8fKnAV_bluTexNyK_JvDUxg9ks5XQ2wlwA%3D%3D
6. source: base_query is starting query point of the xpath for this migration.  We will use //node for this example.
7. We will cover source: attribute in the later part of the tutorial (see If you need to target attributes in the XML file below)
8. source: xpath will be used to create a new array for the migration to read

   ![xpath](https://github.com/poetic/migrate-xml-plugin/blob/development/README%20Screenshots/xpath%20screenshot.png)

   * Refer to the 1 above.  The key is the original source element name of the value we want to migrate.
   * Refer to the 2 above.  The value is the xpath to the content we want to migrate.  Map out the xpath from the path from base_query above. Make sure to replace '/' with '.'.  This will be used as the NEW source element name.
     - attribute/other/sidekick as attribute.other.sidekick

9. source: key is the unique identifier attached to each migrated content.  Insert the NEW source element name here.  Each configuration is allowed to have up to two keys.  Keys cannot be changed when the configuration is updated. ***MAKE SURE THE KEYS ARE ALL LOWERCASE***
10. process: type: default_value is the drupal machine name of the entity the configuration is migrating to. Our content name for this is superhero.
11. Under process, list out the fields that needs to be populated through migration. The key is the machine field name of the node and the value is the NEW element source name from the value we want to access.  Please refer to number 8 for the NEW element source names. ***MAKE SURE THEY ARE ALL LOWERCASE!!!!! ***
12. destination: plugin configures the entity type.  We will use entity:node for this example since our entity is a node (content type).

If you followed these steps, your configuration form should look like this:

![ss1](https://github.com/poetic/migrate-xml-plugin/blob/development/README%20Screenshots/ss1.png)


##Utilizing Process Plugins in Migration Configuration Form
Process plugins are necessary when migration includes any entity references.  We will add two entity references to our configuration form: pets and realname. Both entity references will be added to xpah: just like any other fields.

Under the process: the key will be the machine name just like the other fields.  Unlike other fields, the value will include other attributes, plugin, content_type, source_elements.
  * For plugin, insert entity_reference_plugin if this is a entity reference for a content type and taxonomy_plugin if this is a taxonomy entity reference plugin.
  * For content_type, insert the machine name of the destination
  * For source_element, insert the NEW source element here

If you followed these steps, your configuration form should look like this:

![ss2](https://github.com/poetic/migrate-xml-plugin/blob/development/README%20Screenshots/ss2.png)

##If you need to target attributes in the XML file
Sometimes XML has different attributes with the same elements (see images in the example XML above).

* In this case, we need to update the configuration file on source: attribute.

  ![attribute](https://github.com/poetic/migrate-xml-plugin/blob/development/README%20Screenshots/attribute%20example.png)

  - Refer to the 1 above.  The key doesn't matter here as long as it is not a duplicate.
  - Refer to the 2 above.  The value 2 is the original source element name of the value we want to migrate.
  - Refer to the 3 above.  The value 3 is the exact copy of the attribue from the source xml file. Make sure it is exactly the same.
  - Refer to the 4 above.  The value 4 is the replacement of original source element name.  This will be used as the original source name.

* Go to step 8 from Create Basic Migration Configuration Form above and insert under source: xpath.
* If this was a regular field, it would follow the step 9 from Create Basic Migration Configuration Form above.  Since this is another entity reference (image), we need to use image_plugin.

If you followed these steps, your configuration form should look like this:

![ss3](https://github.com/poetic/migrate-xml-plugin/blob/development/README%20Screenshots/ss3.png)

##Import with Migration
The configuration files is ready be uploaded on Drupal admin page.

1. Configuration/Configuration synchronization/Import tab
2. Choose single item
3. Select Migration
4. Paste in the configuration file

Click on the Export tab to see previous migration configurations.  If you want to override previous configuration, get the uuid from the previous configuration accessed through export tab and include the uuid with the updated configuration file and import it again.

In nebual root level:

* run vagrant ssh
* run cd /var/www/drupal/web
* run migration commands
  - drush cc (clear cache)
  - drush mi migration_id (import)
  - drush mr migration_id (rollback)
  - drush mrs migration_id (reset)
  - drush mi migration_id --update (update)
  - drush mus migration_id (this will unpublish any content missing from XML migrated with this id and publish any unpublished content that is present in XML)
