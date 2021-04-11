---
layout: post
date:   2021-04-11 10:40:00 +0100
categories: OverTheWire Natas
---

# Level 9

```bash
Username: natas10
Password: nOpp1igQAkUzaI1GUUjzn1bFVj7xCNzu
URL:      http://natas10.natas.labs.overthewire.org
```

### As normal, lets look at various sources

![](/assets/41.png)

### I don't believe you, lets see what happens.

![](/assets/42.png)

### Okay, fair. In the source code:

```php
<?  
$key = "";  
  
if(array\_key\_exists("needle", $\_REQUEST)) {  
 $key = $\_REQUEST\["needle"\];  
}  
  
if($key != "") {  
 if(preg\_match('/\[;|&\]/',$key)) {  
 print "Input contains an illegal character!";  
 } else {  
 passthru("grep -i $key dictionary.txt");  
 }  
}  
?>
```

### So this is definately something where you traverse, but can't use any fun characters. Okay, lets yolo and use 'a ls'

![](/assets/43.png)

### That is actually interesting. I wonder if we look at the same path as the previous challenge (and increment by 1) and cat the file..

![](/assets/44.png)

### Nope. Lets try a few more, what could hurt?

![](/assets/45.png)

### Nope

![](/assets/46.png)

### What? Why did that work?

### This is why:

```shell
       -i, --ignore-case
              Ignore  case  distinctions,  so that characters that differ
              only in case match each other.
```

### So the grep command -i will look for any (ignoring case) in the password. The password doesn't contain an A... or a B... But it does contain a C. That's weird.

VICTORY.

```
 U82q5TCMMQ9xuFoI3dYX61s7OZD9JKoK
```
