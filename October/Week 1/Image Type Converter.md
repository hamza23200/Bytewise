# Image Type Converter
* Converting image type from one type to other

# Compressions:
* lossless compression
* lossy compression
* JPEG -> Joint Photographic Experts Group
* PNG -> Portable Network Graphics

```python
from PIL import Image

import glob

print(glob.glob("*.png"))

for file in glob.glob("*.png"):
    im = Image.open(file)
    rgb_im = im.convert('RGB')
    rgb_im.save(file.replace("png", "jpg"), quality=95)
```

```python
import os
for file in glob.glob("*.jpg"):
    os.remove(file)
````
