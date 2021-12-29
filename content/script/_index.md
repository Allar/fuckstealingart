---
title: 'Script'
---

If you had more than one art image stolen, and you're not willing to right-click every single one, you can now run a simple script which fetches all image URLs and extracts them into a readable text file.

### Tutorial for macOS

This is a quick tutorial on how to install Python for macOS
There are of course other ways, but this is the most straight forward one.

1. Open up your terminal by pressing ⌘+Spacebar and searching for terminal.

2. Install [Homebrew](https://brew.sh) by pasting the below script and running it.

`/bin/bash -c "$(curl -fsSL https://raw.githubusercontent.com/Homebrew/install/HEAD/install.sh)"`.

2. Create a new directory, for the sake of the tutorial we'll create one in the Documents folder.

`mkdir Documents/OpenSea/` and then go to that folder `cd Documents/OpenSea/`

3.  Next we'll need to create a new Python file.

`touch opensea.py`
and then open it
`open opensea.py`

5. Copy and paste the following code into the now opened editor.

```python
import json
from haralyzer import HarParser, HarPage

with open('opensea.io.har', 'r') as f:
    har_parser = HarParser(json.loads(f.read()))

data = har_parser.har_data["entries"]
image_urls = []

for entry in data:
    if entry["response"]["content"]["mimeType"].find("image/") == 0:
        image_urls.append(entry["request"]["url"])
     
with open('target_link.txt', 'w') as f:
    for link in image_urls:
        f.write("%s\n" % link)
```

5.1. If you encounter the following error:
```
Traceback (most recent call last):
  File "opensea.py", line 3, in <module>
    from haralyzer import HarParser, HarPage
ImportError: No module named haralyzer
```

you'll need to install haralyzer.

`pip3 install haralyzer`

6. Now go to the thiefs OpenSea profile. Right-click and click on inspect.

7. Go to the network tab (Chrome Browser), refresh the page, and wait for the images to load (on some sites you may have to scroll down to the images for them to start loading).

7. Right click/ctrl click on any entry in the network log, and click on ”Save all as HAR with content”.

8. Run script.