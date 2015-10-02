# vagrantサブコマンド

## init
カレントディレクトリにVagrantの環境を初期化して、  
Vagrantfileを生成  
$ vagrant init  

## box

### box add
Boxファイルの追加  
$ vagrant box add _NAME_ _URL_  

### box list
追加したBoxファイルの一覧表示  
$ vagrant box list  

### box remove
追加したBoxファイルの削除  
$ vagrant box remove _NAME_  

## up
Vagrantfileから仮想マシンの構築、起動  
$ vagrant up  

## destroy
起動している仮想マシンをシャットダウンして、廃棄  
$ vagrant destroy  

## halt
仮想マシンをシャットダウン  
$ halt

## reload
仮想マシンを再起動．halt => upと同等  
$ vagrant reload  

## suspend
仮想マシンをサスペンド  
$ vagrant suspend  

## resume
サスペンドした仮想マシンを復帰  
$ vagrant resume  

## status
仮想マシンの状態を表示  
$ vagrant status  

## ssh
仮想マシンへssh接続
$ vagrant ssh  

## ssh-config
ssh接続の設定を表示
$ vagrant ssh-config  

## provision
起動している仮想マシンにプロビジョニングを実行  
$ vagrant provison  

## plugin

### plugin install
プラグインをインストール  
$ vagrant plugin install _NAME_  
(Ex.)$ vagrant plugin install sahara  

### plugin list
インストールされているプラグインの一覧表示
$ vagrant plugin list  

### plugin uninstall
プラグインをアンインストール  
$ vagrant plugin uninstall _NAME_  

### plugin update
プラグインを更新  
$ vagrant plugin update _NAME_  
(Ex.)$ vagrant plugin update sahara  



## 