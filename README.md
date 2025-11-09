# 　インフラの環境構築

## Kotlin使用のためJavaの設定
### Homebrewのインストール
```
/bin/bash -c "$(curl -fsSL https://raw.githubusercontent.com/Homebrew/install/HEAD/install.sh)"
```
brewコマンド設定
`.zprofile`に以下追加
```
echo 'eval "$(/opt/homebrew/bin/brew shellenv)"' >> /Users/persica/.zprofile
echo >> /Users/persica/.zprofile
eval "$(/opt/homebrew/bin/brew shellenv)"
```
`brew help`でコマンドの一覧出てきたら成功
### JDKのインストール
```
brew install openjdk
```
IntelliJ IDEAなどのGUIアプリケーションがJDKを見つけられるようにシステムのJavaラッパーへの登録
```
sudo ln -sfn /opt/homebrew/opt/openjdk/libexec/openjdk.jdk /Library/Java/JavaVirtualMachines/openjdk.jdk
```
javaコマンドをターミナルで実行できるようにPATH追加
```
echo 'export PATH="/opt/homebrew/opt/openjdk/bin:$PATH"' >> ~/.zshrc
```
設定ファイル（~/.zshrc）を反映
```
source ~/.zshrc
```
```
persica@watanabenoMacBook-Air ~ % java -version // version確認できたらOK                                                                                         
openjdk version "25.0.1" 2025-10-21
OpenJDK Runtime Environment Homebrew (build 25.0.1)
OpenJDK 64-Bit Server VM Homebrew (build 25.0.1, mixed mode, sharing)
```
### mySQLのインストール
```
brew install mysql
```
mysqlサーバーを起動する
```
brew services start mysql
```
rootユーザーにパスワード設定する
```
mysql_secure_installation
```
mysqlサーバーに接続　`mysql -u root -p`で以下のような表示出れば成功
```
persica@watanabenoMacBook-Air momo-infra % mysql -u root -p
Enter password: 
Welcome to the MySQL monitor.  Commands end with ; or \g.
Your MySQL connection id is 13
Server version: 9.5.0 Homebrew

Copyright (c) 2000, 2025, Oracle and/or its affiliates.

Oracle is a registered trademark of Oracle Corporation and/or its
affiliates. Other names may be trademarks of their respective
owners.

Type 'help;' or '\h' for help. Type '\c' to clear the current input statement.

mysql>
```
