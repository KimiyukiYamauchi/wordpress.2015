# wordpress.2015

本リポジトリは夜間クラスのWordpressの授業で使用する

## vagrantによる環境設定
1. VirtualBoxの入手&インストール  
<a href="https://www.virtualbox.org/wiki/Linux_Downloads" target="_blank">ここから入手</a>
1. Vagrantの入手&インストール  
<a href="https://www.vagrantup.com/downloads.html" target="_blank">ここから入手</a>  
<a href="http://blog.raqda.com/vagrant/index.html" target="_blank">Vagrantドキュメント</a>  
<a href="http://www.vagrantbox.es/" target="_blank">vagrantbox.es</a>  
<a href="https://github.com/KimiyukiYamauchi/wordpress.2015/blob/master/vagrant.command.md" target="_blank">vagrantコマンド一覧</a>

## 仮想環境にDebianをインストール手順

1. Debianの入手&インストール  
<a href="https://www.debian.org/" target="_blank">ここから入手</a>
1. 仮想環境の設定
	1. [設定]-[ネットワーク]-[高度]-[ポートフォワーディング]  
	22番と80番を追加  
1. 仮想環境へのssh接続  
$ ssh ユーザ名@localhost
1. リポジトリ/システムの更新  
$ sudo aptitude upgrade  
$ sudo aptitude update  

## サーバ(LAMP)環境構築

1. Apache2インストール&設定
	1. Apache2インストール  
	$ sudo aptitude install apache2  
	1. DocumentRootの所有者をログインユーザに変更  
	$ sudo chown ユーザ名.グループ名 /var/www/html  
1. MySQLインストール&設定
	1. MySQLインストール(インストール途中でデータベース管理者(root)のパスワード設定)  
	$ sudo aptitude install mysql-server  
	1. MySQLサーバへの接続確認(切断は「exit」)  
	$ mysql -u root -p  
	mysql> exit
	1. 設定ファイル(my.cnf)の編集  
		1. ディレクトリの移動  
		$ cd /etc/mysql  
		1. my.cnfのバックアップ  
		$ sudo cp my.cnf my.cnf.bak  
		1. sudo vi my.cnf  
		::: ここから :::  
		[mysqld]  
		character_set_server = utf8  
		skip-character-set-client-handshake  
		default-storage-engine = innoDB  
		innodb_file_per_table  
		[client]  
		default-character-set = utf8  
		[mysqldump]  
		default-character-set = utf8  
		::: ここまで :::  
		1. 設定ファイルの再読み込み  
		$ sudo service mysql reload  