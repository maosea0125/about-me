command  
==========

- 目录及其子目录文件的个数: find ./trunk -type f | wc -l

tar打包压缩
-----------
- tar -cvf /tmp/etc.tar /etc <== 仅打包，不压缩！
- tar -zcvf /tmp/etc.tar.gz /etc <== 打包后，以 gzip 压缩
- tar -jcvf /tmp/etc.tar.bz2 /etc <== 打包后，以 bzip2 压缩