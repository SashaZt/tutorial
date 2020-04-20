FROM centos (скачивание необходимы образ)

RUN yum update -y \ (запускает необходимую команду)
    
    && yum install mc net-tools bind-utils iptables-services chrony ntp epel-release iftop htop atop lsof wget bzip2 traceroute gdisk -y \
    
    && yum install -y cowsay \
    
    && rm -rf /var/cache/yum

ENTRYPOINT ["cowsay"] (выполняет необходимую команду)

В папке с Dockerfile запускаем команду для создание образа

docker build -t sashazt/cowsay .

sashazt - учетная запись на dockerhub

cowsay - название образа

в конце обязательно точку .
