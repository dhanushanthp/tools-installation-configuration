## Monitor Folder Creation
Install ```sudo apt-get install inotify-tools```
```sh
inotifywait -m /usr/local/app/data-logs -e create -e moved_to |
    while read path action file; do
        echo "The file '$file' appeared in directory '$path' via '$action'"
    done
```
