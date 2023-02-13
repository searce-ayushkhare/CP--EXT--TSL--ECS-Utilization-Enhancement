## POC | Enterprise Cloud Search (ESC) Enhancement

### Priorize search results by integrating Keywords

* Select Data Source (for e.g.): 
    * Name : SNTI Journals
    * ID : datasources/<actual_numeric_id> 
* Current indexed document count : <numeric_value>
* Delete data source from Cloud Search (will remove the indexed item from the website)
* Re-define schema with changes (new properties to added done in local repo)
    * File to edit : [schema.json](https://source.cloud.google.com/tsl-cloud-search/snti/+/master:/schema.json)
        ```sh
        {
            "objectDefinitions": [
                {
                    "name": "SNTI",
                    "propertyDefinitions": [],
                    "metadata" : {
                        "contextAttributes": [
                            {
                                "name" : "Subject Collection 2019", 
                                "value" : [
                                    "Engineering",
                                    "Business, Management and Accounting",
                                    "Environmental Science",
                                    "Physics and Astronomy",
                                    "Energy",
                                    "Mathematics"
                                ]
                            },
                            {
                                "name" : "Status", 
                                "value" : [
                                    "Active",
                                    "Incorporated",
                                    "Discontinued"
                                ]
                            }
                        ]
                    }
                }
            ]
        }
        ```

* Register the new schema (command based on code repo file - registerSchema - no other documentation found) 
    ```sh 
    java -Dpayload=./schemaRequest.json -Dapi.serviceAccountPrivateKeyFile=./tata-steel-service-account.json -DrootUrl=https://cloudsearch.googleapis.com -jar schemaRegisterer.jar
    ```
* Re-index the documents (command based on [code repo file - registerSchema](https://source.cloud.google.com/tsl-cloud-search/snti/+/master:/registerSchema) - no other documentation found)
    ```sh
    java -jar google-cloudsearch-csv-connector-v1-0.0.5.jar
    ```
* [If you have an existing Cloud Search implementation, you must re-index your content with named attributes to use this feature](https://developers.google.com/cloud-search/docs/guides/improve-search-quality#increase_ranking_based_on_item_context) ~ Source : Official docs


NOTE : No code repository found in tsl-cloud-search-dev for SNTI-Journal datasource or any other datasource, neither in VM, nor in cloud-source-repository 
Above files are present for prod env.
