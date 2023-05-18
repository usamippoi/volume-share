# 構成
```txt
.
├── docker-compose.yml
└── container1
    ├── Dockerfile
    └── src.txt
├── container2
│   └── Dockerfile
```

# ソース共有を確かめる
```sh
finch compose up -d --build
finch compose logs
```
```txt
container1_1 |src ver 1.0
container2_1 |src ver 1.0
```

# ソースを更新してみる
```txt
- src ver 1.0
+ src ver 1.1
```

# volumeを使い回しているとソースは更新されていない
```sh
finch compose down
docker-compose up -d --build
docker-compose logs
```
```txt
container1_1 |src ver 1.0
container2_1 |src ver 1.0
```

# volumeを削除して作り直すと更新される
```sh
finch compose down
finch volume rm code_share
docker-compose up -d --build
docker-compose logs
```
```txt
container1_1 |src ver 1.1
container2_1 |src ver 1.1
```

# 参考サイト
https://wand-ta.hatenablog.com/entry/2019/02/12/223935  
※一部変更あり