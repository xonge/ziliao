1. ssh-copy-id -i ~/.ssh/id_rsa.pub root@115.29.138.202
1. ssh -p 20086 tiaoban@远程ssh服务器ip    #小p
2. scp -P 20022 src.tar.gz zhouhh@192.168.12.13:/home/zhouhh   #大p
   scp -P 20022 zhouhh@192.168.12.13:/home/zhouhh/src.tar.gz  .
   scp -o port=60066 zhouhh@172.16.22.30:/home/zhouhh/src.tar.gz .
   scp  -P 60066 -r /home/zhouhh/src/.* zhouhh@172.16.22.32:/home/zhouhh/dest/