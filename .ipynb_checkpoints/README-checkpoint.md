# flickr-metadata-reader
Converts a set of JSON formatted flickr image metadata into a single CSV file.
Needs to be tab-delimited, not comma-delimited.
Resulting text file is to be read into Excel for further processing, including:

* Adjust "cabinet names" from 'Cabinet 1' to 'Cabinet 01', etc. to improve sorting results.
* Find and delete any rows that represent images that are not specimens (eg PME logo)
* Generate stats: eg, # blanks for "tags" and "description", # with "0" for lat/long, etc.
* Generate pivot table with counts for each "cabinet" (i.e. Flickr album), including "blank"
* Generate notes, observations, and next steps

Assumes JSON files were downloaded as follows:

* Sign in to the PME Flickr account as owner.
* Click the owner icon - PME icon upper right - and select “Settings”.
* The last left-hand segment of the resulting page is called “Your Flickr Data”. There should be a button called “retrieve data” or “save data” or something similar. 
* Click that button - there should be a message about what will happen. Essentially, Flickr will gather all images into as many 2Gbyte zip files as needed, plus one other zipfile under the Account Data subheading.

Reminder for starting Jupyter

* open a windows powershell
* type "conda activate e211"
* type "cd .\repos\flickr-metadata-reader\"
* type "jupyter notebook"
