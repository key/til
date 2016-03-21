# 3D Connexion SpaceNavigator

CADを触るにあたり何かしらのマウスが必要だったので、 [イギリス帰りのデザイナ](http://www.triplebottomline.cc)がオススメしていた[3Dconnexion SpaceNavigator for Notebook](http://www.amazon.co.jp/gp/product/B0016OOS16/ref=as_li_ss_tl?ie=UTF8&camp=247&creative=7399&creativeASIN=B0016OOS16&linkCode=as2&tag=mitsukuni-22) を購入。

この特殊なマウスは、画面上に表示された3Dモデルを直接的に操作できるよう、XYZ方向に押し・倒しの6軸の操作を行うことが可能。メジャーなCADソフトウェアには軒並み対応しているのも良いところ。

まだCADを触る、というところまで行っていませんが、とりあえず入れてみたRhinoceros, Fusion360, SketchUp, 123D Designでは問題なく動作した。

とはいえ、脳内のXYZ軸とマウスの物理軸が一致しないと混乱するので、CAD上で使うには練習が必要そう。

## Google Eearthで動かない問題

Google Earth (Google Earth Pro含む)でうまく動かないことがあった。どうもドライバやプラグインのバージョンに起因する問題らしい。

いろいろ試した結果、次の組み合わせでうまく動いた。

- MacOSX 10.11.3
- Google Earth Pro 7.1.5.1557
- 3Dconnexion 3DxWare 10 10.1.2

手順は次の通り。プラグインを入れないと動作しなかったので、最後の手順が超重要です。

- 3Dconnexionのサイトから[古いドライバを取得](http://www.3dconnexion.jp/service/archived-drivers.html)する
- 3DxWareをインストール　→　再起動
- System Preferencesを開いてプラグインをインストール
    - `3Dconnexion` を開く
    - `Tools`を選択
    - `Install Plug-ins`をクリックしてプラグインをインストール
- Google Earthを起動する
- マウスをぐりぐりして楽しむ

