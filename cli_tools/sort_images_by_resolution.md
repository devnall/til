# Sort Images By Resolution

This will iterate over a directory of JPEGs and sort them into folders based on and named for their resolutions.

```
#!/bin/bash

for image in *.jpg;
    do res=$(identify -format %wx%h\\n $image);
    mkdir -p $res;
    mv $image $res;
done
```
