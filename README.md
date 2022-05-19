# ShaderGraphIntro
ShaderGraph導入

Shader Graph はノードの接続しグラフを作ることでシェーダを作成することができる
Unity標準のグラフィックツールです。
Shader Graph を用いることでコーディングをしなくても、
多彩な表現のシェーダを作成することが可能になります。

# 導入
Unityのプロジェクトを作成する場合はURPまたはHDRPのテンプレートから作成するとShader Graph が使えます。
（もしくはUnity 2021.2以降であれば従来のBuild-inパイプラインでも使用可能となりました）
画像は2019.4 LTS でUnity Hub から新規プロジェクトを作成する場合です。
![image](https://user-images.githubusercontent.com/1992059/168628228-20773d83-c55a-4e53-833d-78e5f05e76ad.png)

# シェーダの作りかた

URPのサンプルシーン SampleScene で試していきます。
シーン中の作業台に置かれているヘルメットのオブジェクト "Safety Hat" に、シェーダを割り当てたマテリアルを設定して見た目を変えていきます。
![image](https://user-images.githubusercontent.com/1992059/168699568-49a8fd15-00f4-4d82-8aa8-62998ed18dd3.png)

## シェーダ新規作成 
シェーダを新規で作成する場合に選べるメニューはいくつかありますが、
今回は光があたって欲しいオブジェクト用のシェーダにするので、
PBRライティング有りのシェーダで作成していきます。（PBR = 物理ベースレンダリング）
プロジェクトビューで右クリック [Create] - [Sahder] - [PBR Graph]を選択します。
シェーダファイルが新規で作成されファイル名を入力できる状態になるので、今回は"Hat"という名前で進めます。

![image](https://user-images.githubusercontent.com/1992059/168700442-5643952b-7f2e-47d4-9a0b-f3307c9a1826.png)

Hatシェーダが作られました。
![image](https://user-images.githubusercontent.com/1992059/168700532-8c3e5dc7-1b91-4ef4-9dde-7868f096e887.png)

## Shader Graph ビュー

作成したシェーダHatをダブルクリックするとShader Graphの画面がひらきます。

![image](https://user-images.githubusercontent.com/1992059/168700684-35535051-5b93-465e-8d56-b0ebed9ab3ce.png)

まだなにもない白いだけのシェーダですが、いったんこのままマテリアルに割り当ててヘルメットに設定してみます。

## マテリアル作成＆シェーダ設定

プロジェクトビューで右クリックから [Create] - [Material]を選択し、名前を"Hat"とします。
![image](https://user-images.githubusercontent.com/1992059/168699080-aa95933d-ef0a-431f-a2e1-1733627a88d2.png)

生成したマテリアルのインスペクタにてシェーダを選択します。
シェーダのドロップボックスをクリックして[Shader Graphs] - [Hat]と選びます。
これでマテリアルにShader Graphで作ったシェーダが設定されました。
![shader_graph_material_inspector](https://user-images.githubusercontent.com/1992059/169107556-2ca0e99f-42a3-4665-8250-37428a1f2f1c.gif)

## オブジェクトへ設定

用意したマテリアルをヘルメットに設定してみましょう。
シーンビューを表示してヘルメットが見えるようにしておきます。
アセットから作成したマテリアル"Hat"をドラッグして、
シーン中のヘルメットへドラッグ＆ドロップ、これでヘルメットのマテリアルが設定されました。
![shader_graph_assign_material_to_hat](https://user-images.githubusercontent.com/1992059/169108327-a089d905-b71c-4ea7-ae49-e888b19f2825.gif)

シェーダが関連付けられていますので、
今後シェーダを編集して効果をつけた場合も、
シーン中のヘルメットの見た目に変更が効果として反映されていきます。

# テクスチャマッピング

自作のシェーダでヘルメットにテクスチャを貼ってみましょう。
もともとヘルメットに設定されていたテクスチャは以下のパスに有ります。
Assets/ExampleAssets/Textures/Props/HardHat/SafetyHat_Albedo.tif

一連の操作は次のようになります。アニメの↓に解説
![shader_graph_texture_mapping](https://user-images.githubusercontent.com/1992059/169172842-b9816a3f-ad83-4717-9cbe-2c4ca4932a91.gif)

"Hat"シェーダをダブルクリックして Shader Graph の画面を開きます。
空いているところを右クリックするとメニューが出ますので[Create Node]を選択します。
ここからShader Graphで使用できる色々なノードが選択できますが、
今回は"Sample Texture 2D"というテクスチャ画像を読み込むノードを使います。
キーボードで"Text"まで打ち込むとノード名から絞り込みがされて数種のノードだけになるので、
"Sample Texture 2D"を選択します。
ノードの左側に　Texture(T2)と書かれているところに接続されているフィールドが使用するテクスチャになります。
そこをクリックするとプロジェクト内のテクスチャから選択できる"Select Texture"画面が開きます。
ここも"Hat"とキーボードで打ち込むと絞り込みが出来ますので、
黄色いヘルメットのテクスチャSafetyHat_Albedo.tif　を選択します。
![227](https://user-images.githubusercontent.com/1992059/169174246-70ce3a8b-0bdb-4d8d-9cd4-6aefe22eb1a7.png)
これでテクスチャを読み込むノードの設定は出来ました。

"Sample Texture 2D"ノードのRGBA(4)と "PBR Master"ノードのAlbedo(3)という箇所を接続するとシェーダの出力カラーがテクスチャカラーになります。
"PBR Master"ノードはシェーダの最終出力先のノードになります。
"Sample Texture 2D"ノードのRGBA(4)のところの小さな丸のところからドラッグして線をのばし、
"PBR Master"ノードのAlbedo(3)の丸のところに接続します。
![301](https://user-images.githubusercontent.com/1992059/169174542-d4eb29fe-dd2f-48ea-9eb0-1d538523d0fa.png)

これでテクスチャを使ったシェーダは完成しました。
Shader Graph画面左上の"Save Asset"ボタンをクリックしてシェーダを保存し反映させます。

Unityのシーンビューに戻るとヘルメットに黄色いテクスチャが適用されている状態になります。


# 簡単なカラー効果