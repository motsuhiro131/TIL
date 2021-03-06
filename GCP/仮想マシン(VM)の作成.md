VM：AWSでいうEC2のこと  
ここではNGINXを積んだマシンとの接続を行う  
NGINX ：Webサーバーの１つ。負荷が急激に増えない、処理速度が低下しづらい等の特徴がある。  
大量の動的処理は不向きであることが、Apacheとの棲み分けになっている。  
  
## UIで作成する  
### コンソールからVM→Create インスタンスで作成する
- Name：VMの名前を設定する
- Region：リージョンを設定する
- Zone：ゾーンを設定する
- Series：VMマシーンのマシンファミリーを設定する。  
https://cloud.google.com/blog/ja/products/compute/choose-the-right-google-compute-engine-machine-type-for-you
- Machine Type：マシンタイプのCPU等の詳細を設定する
- Boot Disk：OSを設定する
- Firewall：通信の許可を設定する。例えばHTTPは80番ポート等
  
### すべての設定を終えた後に接続をSSHで設定し、アクセス出来ないことを確認する(ただマシンを立ち上げただけなので、空っぽの状態)
- NGINX web serverをインストールする
- SSHターミナルで以下のコマンドを打つ  
```
sudo su -
apt-get update
-- OSのアップデート
apt-get install nginx -y
ps auwx | grep nginx
-- NGINXのインストールと確認
```
http://EXTERNAL_IP/ (EXTERNAL_IPはGUI上のIPアドレス)でトップ画面が出ることを確認する  
  
## gcloudでVMを作成する（CLIと同様）
```
gcloud compute instances create gcelab2 --machine-type n1-standard-2 --zone us-central1-c
```
コンソールで押してた場所は1行で終わり  
```
gcloud compute instances create --help
```
ヘルプの確認に使える（抜ける場合はCtrl C）  
  
```
gcloud compute ssh gcelab2 --zone us-central1-c
--SSHで接続（Yで続行していく）
```
