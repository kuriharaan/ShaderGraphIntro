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

もうすこしグラフを拡張してヘルメットが光る表現を足してみます。

![72](https://user-images.githubusercontent.com/1992059/169214149-fab08406-a2ff-40dd-a1de-af81fe3cbe88.png)

Shader Graph の画面で右クリックから[Create Node]でノード選択メニューにて"Color"と打ち込んでColorノードを配置します。  
Colorノードは任意の色をシェーダで扱えるようにします。  

発光表現など強い光を表現するためにはColorノードの下部の[Mode] を"HDR"とします。  
また、真ん中の色の表示部分をクリックすると色指定メニューが開くので、任意の色を指定してIntensityを1.5くらいにします。  
Intensityの数値が大きいほど強い発光の色になります。  
![image](https://user-images.githubusercontent.com/1992059/169210933-cf8a885c-1acc-4a9e-937c-65828bc27e6c.png)

ColorノードのOut(4)を "PBR Master"ノードの Emmision(3)へドラッグして接続します。    
テクスチャを接続させたAlbedoはライティングの影響をうける表面の色なのに対し、Emissionはライトが暗くてもその色が出力される自己発光の表現となる色の指定になります。  
![image](https://user-images.githubusercontent.com/1992059/169210561-4291ea4a-9444-4a85-bb37-8578d6bd9523.png)

[Save Asset]を行い確認すると、この時点でヘルメットが光っているような見た目になっているかと思います。  
次に時間で明滅するような変化を着けてみましょう。  

Emmisionに接続させるノードグラフを以下の図のように変更します。
![image](https://user-images.githubusercontent.com/1992059/169212104-4f020324-a0c6-4e77-9cb8-1c44cf3ef5cb.png)

まず、下側に３つノードが追加されています。
- Time
- Cosine
- Remap
Timeは実行時間の経過を数値として扱うものです。  
Cosineは三角関数のコサインの値を扱うためのものです。Timeが接続されることで、時間経過にともない-1 ～ 1 の値を緩やかな波型のカーブ状の変化で出力するものになります。  
Remapは数値の範囲を変換させるものです。初期に指定で-1～1 の値を 0 ～ 1の範囲に変換するようになっています。  
これら３つを繋げると、時間経過とともに0～１の範囲で変化する値を出力するようになります。   
あとは[Multiply]ノードに元々の[Color]ノードと[Remap]ノードの出力をつないでいます。
[Multiply]ノードは２つの数値を掛け算するもので、これにより元々のカラーが強くなったり弱くなったりします。  
シーンビューで見ると次のようになっているかと思います（入力がないとシーンビュー画面の更新が止まるので、シーンビュー上でドラッグをすると色が変化するのが分かりやすいと思います）
![shader_graph_emmision_hat](https://user-images.githubusercontent.com/1992059/169210320-27f1896e-11bc-4913-b5c1-1fa54f9c7436.gif)

## その他
Shader Graph の最初の導入としてシェーダを作成してみました。  
今回シェーダ内にテクスチャやカラー情報をそのまま持たせる形で作成しましたが、マテリアルごとにテクスチャやカラーを変更できるようにプロパティを外部に表示して設定できるようにすることも可能です。
色々なノードがあり表現もまだまだあるので、書き足せればと思います。