# sh
auto start php project

#下面是auto_build.sh文件内容

     #!/bin/bash
     ## build src
     echo $1 #project git url
     webroot="/home/project/"
     giturl=$1
     port=$2

     #1、build direct
     dir=$webroot"test"
     if [ ! -d $dir ]; then
     mkdir $dir
     else  
     d="`date +%Y%m%d%H%M%S`"
     cp -r $dir $dir"_"$d
     rm -rf $dir
     mkdir $dir
     fi
     cd $dir

     #2、download project
     #git clone "$1"

     #3、get project name
     last=${giturl##*/}
     project_name=${last%.*}
     echo $project_name

     #4、set nginx config for the project
     ngx_conf=$project_name".conf"
     echo $ngx_conf
     new_conf=$webroot$ngx_conf
     #5、如果没有创建过配置文件
     if [ ! -d $new_conf ]; then
     #创建配置文件
     cp $webroot"/create.conf" $new_conf
     #替换文件内容
     project_url=$webroot$project_name
     sed -i "s/@port@/$port/g" $new_conf 
     sed -i "s/@project_name@/"${project_name}"/g" $new_conf 
     sed -i "s/@server_name@/www.$project_name.com/g" $new_conf 
     fi
     
 #linux crontab每秒执行的最简单实现方法
     
     近要做一个发短信订阅的计划，每3秒执行一次

     * * * * * for i in {0..59}; do curl http://localhost/data/sms_data.php && sleep 3; done;

     每秒执行如下：
     
     * * * * * for i in {0..59}; do curl http://localhost/data/sms_data.php && sleep 1; done;

     每15秒执行一次：

     * * * * * for i in 0 1 2; do curl http://localhost/data/sms_data.php & sleep 15; done;
