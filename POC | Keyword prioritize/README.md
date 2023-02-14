## POC | Enterprise Cloud Search (ESC) Enhancement

### Prioritize search results by integrating Keywords

* Select Data Source (for e.g.): 
    * Name : <datasource_name>
    * ID : datasources/<actual_numeric_id> 
* Current indexed document count : <numeric_value>
* Delete data source from Cloud Search (will remove the indexed item from the website)
* Re-define schema with changes (new properties to added done in local repo)
    * File to edit : [schema.json](https://source.cloud.google.com/tsl-cloud-search/snti/+/master:/schema.json)
        ```sh
        {
            "objectDefinitions": [
                {
                    "name": <data_source_name>,
                    "propertyDefinitions": [],
                    "metadata" : {
                        "contextAttributes": [
                            {
                                "name" : <category1_name>, 
                                "value" : [
                                    <sub-category1>,
                                    <sub-category2>,
                                    ...
                                ]
                            },
                            {
                                "name" : <category2_name>, 
                                "value" : [
                                    <sub-category1>,
                                    <sub-category2>,
                                    <sub-category3>,
                                    ...
                                ]
                            }
                            ...
                        ]
                    }
                }
            ]
        }
        ```

* Register the new schema (command based on code repo file - registerSchema) 
    ```sh 
    <command-to-register-schema-with-command-line-args>
    ```
* Re-index the documents (command based on [code repo file - registerSchema](https://source.cloud.google.com/tsl-cloud-search/snti/+/master:/registerSchema) - no other documentation found)
    ```sh
    java -jar connector_file.jar
    ```
* [If you have an existing Cloud Search implementation, you must re-index your content with named attributes to use this feature](https://developers.google.com/cloud-search/docs/guides/improve-search-quality#increase_ranking_based_on_item_context) ~ Source : Official docs 

* Actual POC document - [CS | Keywords Prioritize](https://docs.google.com/document/d/1SsLgVeOXdgTx41B3pqOYCeAN2SbgNWbIWbT2BvnrKk8/edit)
