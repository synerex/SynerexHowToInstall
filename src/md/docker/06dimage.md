# Dockerfileの作成

### 1. Synerexのソースコードのダウンロード。  
Synerexのソースコードはgithubに公開されているのでクローンする。
``` git
git clone https://github.com/synerex/synerex_alpha.git
```

### 2. Dockerfileを作成する    
ファイル名をDockerfileとし,`./synerex_alpha`のフォルダ直下に配置する
Dockerfileには以下の様に記述する。  
``` Dockerfile
FROM golang:1.13.0-buster

WORKDIR /go/src

# add apt dependencies 
RUN curl -sS https://dl.yarnpkg.com/debian/pubkey.gpg | apt-key add -
RUN echo "deb https://dl.yarnpkg.com/debian/ stable main" | tee /etc/apt/sources.list.d/yarn.list
RUN curl -sL https://deb.nodesource.com/setup_10.x | bash -

# install tools
RUN apt-get update
RUN apt-get -y install zip unzip

# install protocol buffers
RUN curl -OL https://github.com/google/protobuf/releases/download/v3.9.1/protoc-3.9.1-linux-x86_64.zip
RUN unzip protoc-3.9.1-linux-x86_64.zip -d protoc3
RUN mv protoc3/bin/* /usr/local/bin/
RUN mv protoc3/include/* /usr/local/include/
RUN go get -u github.com/golang/protobuf/protoc-gen-go

# install grpc for golang lib
RUN go get -u google.golang.org/grpc

# install nodejs
RUN apt install -y nodejs
RUN apt install -y yarn

# build synerex daemon
WORKDIR /go/src/github.com/synerex/synerex_alpha
COPY . .

# expose port
EXPOSE 8080
EXPOSE 9999
EXPOSE 3000
EXPOSE 10080
```  
このDockerfileをビルドする事によって、Synerexを動作させるのに必要なパッケージもインストールされる。DockerイメージのベースとしてUbuntuのgoインストール済みのイメージをベースとして利用している
**インストールされるパッケージ一覧**
- go言語
- nodejs
- grpc
- yarn

### 3. Dockerfileをビルドしイメージを作成する  
`./synerex_alpha`のフォルダ内で以下のコマンドを実行する
```bash
docker build ./ -t synerex_alpha
```
### 4. 起動する  
`./synerex_alpha`のフォルダ内で以下のコマンドを実行する

```bash
docker run --detach --tty  --name synerex_alpha --rm -v $PWD:/go/src/github.com/synerex/synerex_alpha -p 8080:8080 -p 3000:3000 -p 10080:10080 synerex_alpha
```

起動したら, `docker ps`コマンドでSynerexAlphaのコンテナが起動しているか確認する。

### 5. 起動しているDocker内にアタッチする
以下のコマンドでDockerコンテナにアタッチ出来る。  
```sh
docker exec -it synerex_alpha bash
```
dockerコンテナからデタッチしたい場合は、ctrl+z又はターミナルで`exit`と打つとコンテナから出る事が出来る。

### 6. Synerexのビルドと実行
Dockerコンテナにアタッチした状態で以下のコマンドを実行する。  
```
cd cli/daemon
go build
./se-daemon build
./se-daemon
cd ../se
go build
./se
```

### 6. Dockerを停止させる
以下のコマンドでDockerコンテナに停止する事が出来る。  
```sh
docker stop synerex_alpha
```
