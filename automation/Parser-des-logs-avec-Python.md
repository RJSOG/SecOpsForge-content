# Parser des logs avec Python

> Article de démonstration.

```python
import re
from collections import Counter

FAILED = re.compile(r"Failed password for (?:invalid user )?(\S+) from (\S+)")

with open("/var/log/auth.log") as f:
    hits = Counter(m.group(2) for line in f if (m := FAILED.search(line)))

for ip, count in hits.most_common(10):
    print(f"{ip:15} {count}")
```
