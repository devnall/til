# Sorting Images by Resolution

From https://superuser.com/questions/17562/how-to-sort-images-into-folders-based-on-resolution

This script will sort all images (JPEGs, GIFs, BMPs, PNGs) into folders by resolution.

Super helpful for making sense of a messy Wallpapers folder.

```
#!/bin/bash

shopt -s nullglob # The script spits errors if this is not set and there are, say, no *.png files.
for image in *.jpg *.JPG *.jpeg *.JPEG *.gif *.GIF *.bmp *.BMP *.png *.PNG;
    do res=$(identify -format %wx%h\\n "$image");
    mkdir -p $res;
    mv "$image" $res;
done
```
