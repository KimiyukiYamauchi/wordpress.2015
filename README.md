# wordpress.2015  

本リポジトリは夜間クラスのWordpressの授業で使用する

## vagrantによる環境設定  
1. VirtualBoxの入手&インストール  
<a href="https://www.virtualbox.org/wiki/Linux_Downloads" target="_blank">ここから入手</a>
1. Vagrantの入手&インストール  
<a href="https://www.vagrantup.com/downloads.html" target="_blank">ここから入手</a>  
<a href="http://blog.raqda.com/vagrant/index.html" target="_blank">Vagrantドキュメント</a>  
<a href="https://docs.vagrantup.com/v2/" target="_blank">Vagrantドキュメント(英語版)</a>  
<a href="http://www.vagrantbox.es/" target="_blank">vagrantbox.es</a>  
<a href="https://github.com/KimiyukiYamauchi/wordpress.2015/blob/master/vagrant.command.md" target="_blank">vagrantコマンド一覧</a>  
VirtualBox用Cenot6.4のBoxファイル: https://dl.dropboxusercontent.com/u/3657281/centos64_ja.box  

## 仮想環境にDebianをインストール手順  

1. Debianの入手&インストール  
<a href="https://www.debian.org/" target="_blank">ここから入手</a>
1. 仮想環境の設定(VitrualBox側)  
	1. [設定]-[ネットワーク]-[高度]-[ポートフォワーディング]  
	以下の追加  
	ホストポート 2222 ゲストポート 22  
	ホストポート 8080 ゲストポート 80  
	1. [設定]-[ネットワーク]  
	「アダプター２」に「ホストオンリーアダプタ」を設定
1. ネットワークの設定(Debian側)  
	1. 「アダプタ－２」の設定を追加  
	＃vi /etc/network/interface  
	::: ここから追加 :::  
	auto eth1  
	iface eth1 inet static  
	address 192.168.33.10  
	netmask 255.255.255.0  
	::: ここまで追加 :::  
	2. ネットワークの再起動  
	＃service networking restart  
1. 仮想環境へのssh接続  
$ ssh ユーザ名@localhost  
$ ssh -p 2222 ユーザ名@127.0.0.1  
$ ssh ユーザ名@192.168.33.10  
1. リポジトリ/システムの更新  
＃aptitude upgrade  
＃aptitude update  
1. sudoコマンドを使えるようにする  
	1. sudoコマンドインストール&設定  
	＃aptitude install sudo  
	＃vi /etc/group  
	「sudo:」にログインユーザを追加  
	1. 一旦exitし、sshに接続し直す  
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
		1. エディタで開いて編集  
		$ sudo vi my.cnf  
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
		$ sudo service mysql restart  
1. PHPイストール&設定  
	1. phpパッケージのインストール  
	$ sudo aptitude install php5  
	1. MySQLとの連携のためのパッケージのインストール  
	$ sudo aptitude install php5-mysql  
	1. その他のパッケージのインストール  
	$ sudo aptitude install php-pear php5-gd  
	1. Apacheの再起動(phpを読み込むため)  
	$ sudo service apache2 restart  
	1. 動作確認  
		1. エディタでphpファイルを作成  
		$ vi /var/www/html/test.php  
		::: 以下を追加 :::  
		<?php  
			phpinfo(); // phpの設定情報表示  
		?>  
		::: 以上を追加　:::  
		1. ブラウザで以下にアクセスし、phpの設定情報が表示されること  
		http://192.168.33.10/test.php  
	1. 設定ファイル(php.ini)の編集
		1. ディレクトリの移動  
		$ cd /etc/php5/apache2  
		1. php.iniのバックアップ  
		$ sudo cp php.ini php.ini.bak  
		1. エディタで開いて編集  
		$ sudo vi php.ini  
		::: ここから :::  
		display_errors = On  
		error_log = /var/log/php.log  
		mbstring.language = Japanese  
		mbstring.internal_encoding = UTF-8  
		mbstring.http_input = auto  
		mbstring.detect_order = auto  
		expose_php = Off  
		date.timezone = Asia/Tokyo  
		::: ここまで :::  
		1. Apacheの再起動(設定ファイルの再読み込みのため)  
		$ sudo service apache2 restart  