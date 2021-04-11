---
layout: post
date:   2021-04-11 10:20:00 +0100
categories: OverTheWire Natas
---

# Level 8

```bash
Username: natas8
Password: DBfUBfqQG69KvJvJ1iAbMoIpwSNQ9bWe
URL:      http://natas0.natas.labs.overthewire.org
```

![](/assets/28.png)


![](/assets/29.png)

## Mmmmkay. So I need to:
1. Install WAMP
2. base64_decode. 
3. strrev
4. hex2bin

### Here's the script

```php
<?php

$encodedSecret = "3d3d516343746d4d6d6c315669563362";

function decodeSecret($secret) {

 return base64\_decode(strrev(hex2bin($secret)));

}

echo decodeSecret($encodedSecret);

?\>
```
 
 ### A WAMP install and PHP script later..

![](/assets/27.png)
![](/assets/30.png)
![](/assets/31.png)


VICTORY.

```
W0mMhUcRRnG8dcghE4qvk3JA9lGt8nDl 
```
