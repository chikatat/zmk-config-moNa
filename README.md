## 3. 動作確認

### 3-1. 組み立て

1. トッププレートについているねじをすべて外し、トッププレートを外してください。
2. トッププレートの角にいくつかキースイッチをはめ込み、PCBに差し込みます。
3. ほかのキースイッチもすべてはめ込み、キーキャップを取り付けたら完成です。

### 3-2. PCとの接続方法
1. それぞれのマイコンのリセットボタンを1回押します。
2. PCでbluetoothデバイスとして「moNa」を選択します。

bluetooth接続が完了したらすべてのキーが認識するか、ロータリーエンコーダ、トラックボールが問題なく動作するか確認してください。
左右間のペアリングは電源を入れると自動的に行われます。
有線接続でも動作しますが、左右間は無線接続のみになります。
ロータリーエンコーダ側はPCに有線接続してもキーボードとして動作しません。

### 3-3. LEDの簡易表示について
左右のマイコンについているLEDで2つの状態を確認することができます。
#### バッテリー残量
* 起動時にバッテリー残量に応じて🟢/🟡/🔴で点滅（中央側・周辺側の両方で）
* 重要なバッテリー残量を下回ると🔴で点滅

#### Bluetooth接続状況
* bluetoothプロファイルの切り替え時、接続状態に応じて🔵/🟡/🔴で点滅


## 4. ファームウェアについて

### 4-1. キーマップの編集

冒頭で書いたようにzmk firmwareの編集にはgithubのアカウントが必要です。  
一からファームウェアを用意する際の手順は[公式ドキュメントの導入解説](https://zmk.dev/docs/user-setup)を見るとわかりやすいです。  
以下では、私が作成したリポジトリをフォークし、[KeymapEditor](https://nickcoutsos.github.io/keymap-editor/)を用いてGUIでキーマップを書き換える手順を紹介します。  

1. githubアカウントを作成し、ログインします。
2. [このリポジトリ](https://github.com/sayu-hub/zmk-config-moNa)にアクセス
3. 画面右上の「Fork」をクリック
![](img/fork.png)
4. そのまま「Create fork」をクリック
![](img/createfork.png)
5. フォークしたリポジトリの「Actions」タブに移動し、「I understand my workflows, go ahead and enable them」をクリックし、github Actionsを有効化
![](img/enableActions.png)
6. [KeymapEditor](https://nickcoutsos.github.io/keymap-editor/)にアクセス  
7. 「GitHub」を選択
![](img/keymapeditor1.jpg)
8. 「Login with GitHub」からでログイン 
9. 「Only select repositories」を選択して「ADD Repository」を押す
![](img/addrepository.png)
10. 「Only select repositories」を選択し「Selectrepositories」から「zmk-config-moNa」を選択して「Install」を押す
![](img/selectrepository.png)
11. Keymap Editor上でキーマップが表示されたら、好きにキーマップを編集する
12. 画面左上の「Save」を押すと、編集したキーマップが適用されてGitHub Actionsが走り、自動的にビルドが開始します
![](img/keymapeditor2.jpg)
13. 「Save」の隣に表示される「Latest」をクリックするとGitHubに移動し、ビルドが完了するとファームウェアがダウンロードできるようになります。  
 (ビルドには2~4分かかる場合があります。)
14. [書込み手順](#4-2ファームウェアの書き込み方法)に従い、ファームウェアを書き込みます。  
    + キーマップの編集のみの場合はトラックボール側(セントラル)のみを書き換えることで変更が適用されます。  
    リセットファームウェアの書込みも基本的には必要ありません。
    + KeymapEditorを用いずにmoNa.keymap以外のファイルの内容を書き換えた場合は、左右のファームウェアを書き換えてください。  
    + ファームウェアを書き直した際は、PC側のペアリング情報も削除してから再度ペアリングを行ってください。
15. 無事に変更したキーマップが適用されていれば成功です。

### 4-2.ファームウェアの書き込み方法

1. PCと左側のマイコンをUSBで接続します。はじめはキーボードの電源はオフで大丈夫です。
2. マイコンのリセットボタンを2回押すと、「XIAO SENSE」という名前でUSBドライブとして認識されるかと思います。(ブートローダの起動)
3. 「XIAO SENSE」ドライブにsettings_reset-seeeduino_xiao_ble-zmk.uf2をドラッグアンドドロップします。  
4. 書込み完了すると、「XIAO SENSE」というドライブは消えますが、再度セットボタンを2回押し、ブートローダを起動します。  
5. 「XIAO SENSE」ドライブにmoNa_L rgbled_adapter-seeeduino_xiao_ble-zmk.uf2をドラッグアンドドロップします。  
6. 右側も同様の手順でsettings_reset-seeeduino_xiao_ble-zmk.uf2とmoNa_R rgbled_adapter-seeeduino_xiao_ble-zmk.uf2を順番に書き込みます。
7. 両方の書込みが完了したら、電源を入れ、それぞれのマイコンのリセットボタンを**1回**押します。
8. PCでbluetoothデバイスとして「moNa」が認識され接続できればOKです。  

