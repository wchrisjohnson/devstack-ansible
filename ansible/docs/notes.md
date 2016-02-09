## Overview

### Manually test your ansible environment

```
ansible all \
  --private-key /Users/wchrisjohnson/.vagrant.d/insecure_private_key \
  -u vagrant \
  -i ansible/inventory/dev \
  -a "/bin/echo hello"
```