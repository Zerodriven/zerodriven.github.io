---
layout: post
date:   2021-04-11 10:40:00 +0100
categories: OverTheWire Natas
---

# Level 11

```bash
Username: natas11
Password: nOpp1igQAkUzaI1GUUjzn1bFVj7xCNzu
URL:      http://natas10.natas.labs.overthewire.org
```

### As normal, lets look at various sources

![](/assets/47.png)

### Okay.. I'm going to look at the source for this one, this looks interesting.

```php
<?  
  
$defaultdata = array( "showpassword"=>"no", "bgcolor"=>"#ffffff");  
  
function xor_encrypt($in) {  
 $key = '<censored>';  
 $text = $in;  
 $outText = '';  
  
 // Iterate through each character  
 for($i=0;$i<strlen($text);$i++) {  
 $outText .= $text[$i] ^ $key[$i % strlen($key)];  
 }  
  
 return $outText;  
}  
  
function loadData($def) {  
 global $_COOKIE;  
 $mydata = $def;  
 if(array_key_exists("data", $_COOKIE)) {  
 $tempdata = json_decode(xor_encrypt(base64_decode($_COOKIE["data"])), true);  
 if(is_array($tempdata) && array_key_exists("showpassword", $tempdata) && array_key_exists("bgcolor", $tempdata)) {  
 if (preg_match('/^#(?:[a-fd]{6})$/i', $tempdata['bgcolor'])) {  
 $mydata['showpassword'] = $tempdata['showpassword'];  
 $mydata['bgcolor'] = $tempdata['bgcolor'];  
 }  
 }  
 }  
 return $mydata;  
}  
  
function saveData($d) {  
 setcookie("data", base64_encode(xor_encrypt(json_encode($d))));  
}  
  
$data = loadData($defaultdata);  
  
if(array_key_exists("bgcolor",$_REQUEST)) {  
 if (preg_match('/^#(?:[a-fd]{6})$/i', $_REQUEST['bgcolor'])) {  
 $data['bgcolor'] = $_REQUEST['bgcolor'];  
 }  
}  
  
saveData($data);  
  
  
  
?>
```

### This line looks interesting to me. Is the cookie the key? I'm going to have to copy this PHP and do some tweaks..,

```php
$tempdata = json_decode(xor_encrypt(base64_decode($_COOKIE["data"])), true);  
```

### I'm going to do some stuff.. To be continued.



```
 
```
