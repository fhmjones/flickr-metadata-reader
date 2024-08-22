# flickr-metadata-reader
Converts a set of JSON formatted flickr image metadata into a single CSV file.
Assumes JSON files were downloaded as follows:

* Sign in to the PME Flickr account as owner.
* Click the owner icon - PME icon upper right - and select “Settings”.
* The last left-hand segment of the resulting page is called “Your Flickr Data”. There should be a button called “retrieve data” or “save data” or something similar. 
* Click that button - there should be a message about what will happen. Essentially, Flickr will gather all images into as many 2Gbyte zip files as needed, plus one other zipfile under the Account Data subheading.
