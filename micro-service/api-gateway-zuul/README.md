注意：要配置 hosts 文件，进行映射
```
127.0.0.1 www.shenjy.com
```

# build.sh 不能运行

```
-bash: ./build.sh: /bin/bash^M: 坏的解释器: 没有那个文件或目录
vim build.sh
:set ff=unix
:wq
```

# docker 运行

```
docker run -it api-gateway-zuul:latest
```