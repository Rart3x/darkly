# Exploit 13 - htaccess

The url http://192.168.56.101/robots.txt inform us that there exists
two _hidden_ urls:

-   /whatever
-   /.hidden

Under http://192.168.56.101/whatever/htpasswd we can retrieve the admin password:

-   root:437394baff5aa33daa618be47b75cb49

It looks like a md5 hash, it's reversible:

with the help of https://md5.gromweb.com/?md5=437394baff5aa33daa618be47b75cb49
we reverse the hash into _qwerty123@_

Those credentials do not work on the sign in page, there must be an admin page:

Found at http://192.168.56.101/admin

Finally the flag retrieval can be automated with the command:

```bash
curl -s -X POST http://192.168.56.101/admin/ --data "username=root&password=qwerty123@&Login=Login" | grep -oP 'The flag is : \K[0-9a-f]{64}'

```
