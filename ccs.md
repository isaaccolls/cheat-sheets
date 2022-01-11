# build on docker alias

```bash
alias ccsc=_ccsc_func
_ccsc_func() {
    file=$1
    if [ "$file" != "" ]; then
        route=$PWD/$file
        echo "going to build: $file"
        if [ -f "$route" ]; then
            echo "$route is real!"
            container="picc"
            if [[ "$(docker inspect -f '{{.State.Running}}' $container)" == "true" ]]; then
                ccscLocation="/opt/picc"
                echo "copying file to container"
                docker cp $route $container:$ccscLocation/temporal/
                echo "start building!"
                docker exec $container bash -c "$ccscLocation/ccsc +fm $ccscLocation/temporal/$file"
                echo "get files"
                docker cp $container:$ccscLocation/temporal/. $PWD
                echo "end!"
            else
                echo "container isn't running"
            fi
        else
            echo "$file doesn't exist"
        fi
    else
        echo "file.c missing!!"
    fi
}
```