---
jupyter:
  jupytext:
    formats: ipynb,md
    text_representation:
      extension: .md
      format_name: markdown
      format_version: '1.3'
      jupytext_version: 1.14.0
  kernelspec:
    display_name: Python 3 (ipykernel)
    language: python
    name: python3
---

To test multifile reading of JSON files representing Flickr image metadata

```python
import json
import os

# Folder Path
path = "data"
os.chdir(path)
count=0

print(os.getcwd())

#open blank CSV file
#NOTE the encoding may not be correct, but leaving this off results in crash when there is a Romanian location.
#This happens with file "photo_32825732587.json", 
outf = open("demofile.csv", "w", encoding="utf-16") #re-write, NOT appending.

#print CSV file's top row
#NOTE: use tabs not commas to avoid confusion when Excel opens the CSV file
outf.write("name\tPMElocn\tflickrpage\timageurl\taccuracy\tlat\tlong\ttags\tdescription\tcount_views\tcount_faves\tcount_comments\tdate_taken\tdate_imported\tlicense\tprivacy\n")
#file is now open, don't forget to close it.
```

```python
# Read JSON File 

for file in os.listdir(): 
    # Check whether file is a JSON file 
    if file.endswith(".json"):         
        file_path = f"{os.getcwd()}/{file}"
        inf = open(file_path, 'r')
        data = json.load(inf)
        
        #pick out parameters
        name = data["name"]
        photopage = data["photopage"]
        original = data["original"]
        count_views = data["count_views"]
        count_faves = data["count_faves"]
        count_comments = data["count_comments"]
        date_taken = data["date_taken"]
        date_imported = data["date_imported"]
        license = data["license"]
        privacy = data["privacy"]
        
        #description may have unwanted newline characters:
        descr = data["description"]
        descrip = descr.replace("\n\n", "\n")
        description = descrip.replace("\n", ", ")

        #pick out lat/long/accuracy - a list
        latlon = data["geo"]
        
        if len(latlon) < 1:
            lat = 0
            lon = 0
            acc = 0
        else:
            lat = latlon[0]['latitude']
            lon = latlon[0]['longitude']
            acc = latlon[0]['accuracy']
        
        #pick out cabinet - an array of lists
        #could be >1, but ideally specimens should be in only one album (i.e. one PME cabinet)
        album_array = data["albums"]
        i = len(album_array)
        PMElocn = ""

        for x in range(i):
            PMElocn += album_array[x]["title"]
            if x<i-1:
                PMElocn += ", "
        
        #pick out tags - an array of lists
        tag_array = data["tags"]
        i2 = len(tag_array)
        tag_list = ""

        for x in range(i2):
            tag_list += tag_array[x]["tag"]
            if x<i2-1: 
                tag_list += ", "
        
        #concatenate the components for a row in the CSV file
        #NOTE: use tabs not commas to avoid confusion when Excel opens the CSV file
        string = f"\"{name}\"\t\"{PMElocn}\"\t{photopage}\t{original}\t{acc}\t{lat}\t{lon}\t\"{tag_list}\"\t\"{description}\"\t{count_views}\t{count_faves}\t{count_comments}\t\"{date_taken}\"\t\"{date_imported}\"\t\"{license}\"\t\"{privacy}\"\n"
        
        outf.write(string)
        count = count+1
        #print(count)

#save and close the file
outf.close()
print(f"{count}","files processed.")
```

```python

```
