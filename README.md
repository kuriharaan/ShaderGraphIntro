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

まだなにもない白いだけのシェーダですが、いったんこのままマテリアルに割り当ててバケツに設定してみます。

## マテリアル作成＆シェーダ設定
![image](https://user-images.githubusercontent.com/1992059/168699080-aa95933d-ef0a-431f-a2e1-1733627a88d2.png)

## オブジェクトへ設定



# テクスチャマッピング

# 簡単なカラー効果