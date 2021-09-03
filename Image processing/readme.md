---
description: Image processing tricks
---

# Bulk image compression
```bash
$ find . -name '*.JPG' | sed 's#.*/##' | xargs -n1 -P8 -I{} convert -resize 15% "{}" "opt-{}"
```

{% hint style="info" %}
This will compress all the files with extension JPG to 15% of the original size
{% endhint %}