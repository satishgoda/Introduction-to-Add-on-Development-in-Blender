
<div id="sect_title_img_0_0"></div>

<div id="sect_title_text"></div>

# はじめに

<div id="preface"></div>

###### 　

{% if book.edition >= 2.0 %}
{% if book.format == "pdf" %}

## 第2版執筆にあたって

初版の執筆を終えた時、初めて本という形でものを作り上げたことの達成感は非常に大きいものがありました。しかし執筆後に本書を再び読み返してみると、アドオンをこれから開発する人にとって本当に必要な情報が抜けているのではないかと思うようになりました。特に第2版で追加したUIの制御は、UIを個人向けにカスタマイズする時などの比較的初心者でも扱う機会の多い話題であるにもかかわらず、初版ではほとんど触れていませんでした。

第2版では誤字の修正をはじめとして、筆者が初版で不足していると感じた話題を新たに執筆しました。また第2版では、基本的な内容である1章と2章から構成される前編と、多少応用的な内容を扱っている3章と4章から構成される後編に分けました。本来であれば分冊にせず1冊でまとめたほうが良いのですが、ページ数の関係上このような形をとらせていただきました。

{% if book.volume == "1" %}

第2版の前編に追加した内容を以下にまとめましたので、必要に応じて参考にしてください。なお初版と同様、サンプルを用いて実際に手を動かしながら理解していく方針で説明しています。

* より詳細なアドオンのインストール方法・アンインストール方法・アップデート方法（[1-4節](body/chapter_01/04_Understand_Install_Uninstall_Update_Add-on.md)）
* アドオンのソースコードを複数のファイルに分割する方法（[2-7節](body/chapter_02/07_Divide_Add-on_Source_into_Multiple_Files.md)）
* BlenderのUI制御方法（[2-8節](body/chapter_02/08_Control_Blender_UI_1.md)、[2-9節](body/chapter_02/09_Control_Blender_UI_2.md)、[2-10節](body/chapter_02/10_Control_Blender_UI_3.md)）

{% elif book.volume == "2" %}

{% endif %}

{% endif %}
{% endif %}

## 本書について

def execute(self, context):

本書は、3DCGソフト「Blender」のアドオンを初めて開発する方を対象とした、アドオン開発の入門書です。
本書を最後まで読むことでアドオンとは何かを理解できるだけでなく、アドオンを開発する際に最低限必要な知識を身につけ、各自で独自のアドオンを開発することができるようになります。

本書はアドオン開発の経験がない方を対象とすると書きましたが、すでにアドオンの開発を経験されている方でも参考になる情報があると考えています。特に最終章では、アドオンの公開方法やデバッグ方法、作ったアドオンをBlender本体に取り込んでもらう方法などのアドオンに関連した話題も取り上げています。アドオンの開発には直接役立たないかもしれませんが、知っておくと後々役立つと思われる情報であると思いますので、余力があればぜひ一読ください。

### Blenderのアドオン開発って面白いの？

筆者は、3Dゲームを開発中に3DモデルをBlenderで作成していた知人から、Blenderへの新規機能の追加を頼まれたことがきっかけでアドオン開発の世界に入りました。

初めて作成したアドオンは、View3D上で選択した面間のUVをコピー・ペーストするというものでした。Blenderで作成した3Dモデルにテクスチャを設定する時、最近は直接ペイントしたり自動的にUV展開することが多くなりつつありますが、頂点数を少なくして応答性を高めるゲーム分野では、いまだにUVを意識する必要があります。ゲーム開発中にゲームで使用する3Dモデルを作成している知人から、BlenderにUVをコピーする機能がなく困ってるという話を聞いたことでアドオンを開発することになりました。

初めてのアドオン開発ということもありいろいろ苦労しましたが、無事に記念すべき第1弾となるアドオンが完成しました。作ったアドオンを使った知人から便利だと感想をもらった時は、作成に苦労した分非常に嬉しかったです。自分で作成したアドオンを使ったユーザから感想をもらえるのは嬉しく、楽しいものです。そして、アドオン開発を通して他のアドオン開発者やアドオン利用者と交流できるのも、アドオン開発の醍醐味の一つだと思います。

ちなみに最初に作成したアドオンは、Web上で様々な意見を取り入れることで改善が進み、UVのコピー・ペースト機能以上の機能を持つようになりました。アドオンを公開することで、自分で開発したアドオンがより強力な機能を持つようになっていくのは、非常に面白いですね。

### 本書をなぜ執筆したの？

筆者自身、アドオン開発を始めた当時はBlenderの標準の機能ですら使い慣れていない状態でした(今もですが)。このため、初めてアドオンを開発した時はどこから手をつけたら良いかわからず、手探りで開発を進めるしかありませんでした。そして当時はアドオン開発の解説サイトが今以上に少なく、さらに日本語をサポートしているWebサイトとなると数を数えられるくらいのWebサイトしかありませんでした。結局他のアドオンのソースコードを読んで改造してデバッグしながらなんとか完成させたのですが、想像していたよりも開発に時間がかかってしまいました。そんな中、アドオンを開発しようと考えている人が同じ苦労をして欲しくないと思い、本書の執筆を決めたのです。

さらに、これまでBlenderを3DCGを作るためのツールとしてのみ使ってきた方にも、本書を読んでアドオンの開発に挑戦してもらいたいという期待があります。実際、3DCGを作るためにBlenderを利用するユーザは、開発者が意識していないような改善案や問題意識をBlenderに対して持っていることが多い気がします。本書を読むことで、これまでBlenderを使う立場であった方がアドオン開発に一歩踏み出せたらと思います。

## 本書の読み方

本書ははじめてBlenderのアドオンを開発する方を対象としているため、Blenderやアドオンとは何かという説明から始めています。すでにBlenderを使ったことがある方にとって、前半の解説は当たり前すぎて物足りないと感じると思います。本書は前から後ろに進んでいくにつれて、基本的な内容から発展的な内容になるように構成を意識して執筆していますので、必要に応じて飛ばし読みしていただいても問題ありません。また、本書は節ごとにテーマを決めて解説する構成を取っているので、知りたい内容に絞って読んでも良いです。

本書は、読者の方が実際に手を動かして作業する場面が数多くあります。本を読んだだけでは理解できていないことがよくありますので、ぜひ積極的に手を動かしてみましょう。特にアドオンのサンプルを用いて説明している節では、必ずお手元の環境で動作させて確認するようにしてください。サンプルをそのまま動かすだけでも、いろいろ学べることはありますよ。

それでは、楽しいBlenderアドオン開発の世界を満喫してください！

## 本書で紹介するサンプルのソースコードについて

本書で紹介するアドオンのサンプルのソースコードは、以下のURLからダウンロードすることができます。

{% if book.edition == 1.0 %}

https://github.com/nutti/Introduction-to-Add-on-Development-in-Blender/releases/download/v1/sample_v1.zip

または

https://github.com/nutti/Introduction-to-Add-on-Development-in-Blender/tree/v1/sample/src

{% elif book.edition == 2.0 %}

https://github.com/nutti/Introduction-to-Add-on-Development-in-Blender/releases/download/v2/sample_v2.zip

または

https://github.com/nutti/Introduction-to-Add-on-Development-in-Blender/tree/v2/sample/src

{% endif %}



## 前提知識

本書を読むための必須知識と、より高度なアドオンを開発するための推奨知識を示します。

### 必須知識

本書を読むために必要となる必須知識は以下の通りです。

* Blenderの基礎知識
  * 基本操作
* Pythonの基礎知識
  * 変数（変数宣言、値の代入、型）
  * 四則演算
  * オブジェクト（タプル、リスト、辞書）
  * 関数（関数定義、呼び出し、戻り値）
  * クラス（クラス定義、メンバ変数、メソッド、継承）
  * モジュールのインポート
* 3DCGの知識
  * 基本用語（メッシュ、UV座標、面、法線など）


### 推奨知識

必須知識に加えて以下の知識があると、本書で紹介している以上の高度なアドオンを作成することができると思います。
なお本書を読むだけであれば、必ずしも必要ではない知識です。

* 数学
  * 三角関数
  * ベクトル演算
  * 行列演算
* 物理
  * 古典力学
  * 流体力学
* 英語
  * 3DCG関連の英語
  * 日常会話で利用する英語(チャット)

{% include "LICENSE" %}

## 誤字・脱字を報告いただける方について

本書内の誤字・脱字を発見された方は、以下のサポートページや [おわりに](body/Conclusion.md) に記載している連絡先よりご連絡ください。

https://github.com/nutti/Introduction-to-Add-on-Development-in-Blender/issues
https://www.gitbook.com/book/nutti/introduction-to-add-on-development-in-blender/discussions

また、本書の原本が置かれているGitHubページからPull Requestを出すことにより、各自修正した内容について反映依頼を出すことができます。

https://github.com/nutti/Introduction-to-Add-on-Development-in-Blender

なお本書の執筆に貢献いただいた方は、許可を取った上で謝辞に名前(またはニックネーム)を掲載させていただきます。

## 本書へのリクエストについて

本書に追加を希望する話題等がある場合、以下のサポートページや [おわりに](body/Conclusion.md) に記載している連絡先よりリクエストを出すことができます。

https://github.com/nutti/Introduction-to-Add-on-Development-in-Blender/issues
https://www.gitbook.com/book/nutti/introduction-to-add-on-development-in-blender/discussions


## 本書の内容に関するお問い合わせについて

本書の内容に関する問い合わせについては、以下のサポートページや [おわりに](body/Conclusion.md) に記載している連絡先から問い合わせください。

https://github.com/nutti/Introduction-to-Add-on-Development-in-Blender/issues
https://www.gitbook.com/book/nutti/introduction-to-add-on-development-in-blender/discussions
