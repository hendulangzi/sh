# sh
auto start php project

#下面是auto_build.sh文件内容
    #!/bin/bash
    ## build src
    echo $1 #project params url

    #build direct
    if [ ! -d "/home/project/test" ]; then
    mkdir /home/project/test
    fi
    cd /home/project/test/

    #download project
    #git clone "$1"

    #get project name
    giturl=$1
    last=${giturl#*/}
    project_name=${last%.*}
    echo $project_name

    #set nginx config for the project
