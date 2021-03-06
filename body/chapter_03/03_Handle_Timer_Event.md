<div id="sect_title_img_3_3"></div>

<div id="sect_title_text"></div>

# タイマのイベントを扱う

<div id="preface"></div>

###### [3-1節](01_Handle_Mouse_Click_Event.md) と [3-2節](02_Handle_Keyboard_Key_Event.md) でユーザからの入力イベントを扱いましたが、アドオンでは他にもタイマを設定してある時間が経過した時にイベントを発生させることができます。本節では、タイマから発生するイベントを扱う方法を紹介します。

## 作成するアドオンの仕様

* *3Dビュー* エリアのプロパティパネルの *一定間隔でオブジェクトを移動* に、オブジェクトを一定間隔で移動するモードを開始/終了するためのボタンを配置する
  * オブジェクトモードかつ、選択中のオブジェクトがメッシュ型の場合のみ表示する
* オブジェクトを一定間隔で移動するモードでは、選択したオブジェクトについて開始ボタンを押した時の位置を中心とし、一定間隔で円を描くように移動する


## アドオンを作成する

[1-5節](../chapter_01/05_Install_own_Add-on.md) を参考にして以下のソースコードを入力し、ファイル名を ```sample_3_3.py``` として保存してください。


[import](../../sample/src/chapter_03/sample_3_3.py)

## アドオンを使用する

### アドオンを有効化する

[1-5節](../chapter_01/05_Install_own_Add-on.md) を参考に、作成したアドオンを有効化するとコンソールウィンドウに以下の文字列が出力されます。

```sh
サンプル3-3: アドオン「サンプル3-3」が有効化されました。
```

<div id="sidebyside"></div>

|また、プロパティパネルの *一定間隔でオブジェクトを移動* にボタンが配置されます。|![3-3節 アドオン有効化](https://dl.dropboxusercontent.com/s/18venqljmdtefp3/enable_add-on.png "3-3節 アドオン有効化")|
|---|---|



### アドオンの機能を使用する

<div id="process_title"></div>

##### Work

<div id="process"></div>

|<div id="box">1</div>|*3Dビュー* エリアのプロパティパネルの *一定間隔でオブジェクトを移動* に配置されている *開始* ボタンを押します。|![3-3節 アドオンの使用 手順1](https://dl.dropboxusercontent.com/s/t6gn930juq6fh1n/use_add-on_1.png "3-3節 アドオンの使用 手順1")|
|---|---|---|

<div id="process_sep"></div>

---

<div id="process"></div>

|<div id="box">2</div>|選択中のオブジェクトが約0.1秒ごとに、開始ボタンを押した時の位置を中心に円を描くように移動します。|![3-3節 アドオンの使用 手順2](https://dl.dropboxusercontent.com/s/fk84kkwzwtzyu7j/use_add-on-2.png "3-3節 アドオンの使用 手順2")|
|---|---|---|

<div id="process_sep"></div>

---

<div id="tips"></div>

開始ボタンを押した後もオブジェクトを移動することができますが、タイマイベントを契機に元の場所に戻ります。

<div id="process"></div>

|<div id="box">3</div>|*終了* ボタンを押すとオブジェクトの移動しなくなり、開始ボタンを押した時の位置にオブジェクトが移動します。|![3-3節 アドオンの使用 手順3](https://dl.dropboxusercontent.com/s/ori4aazvlzoxhlf/use_add-on-3.png "3-3節 アドオンの使用 手順3")|
|---|---|---|

<div id="process_sep"></div>

---

<div id="process_start_end"></div>

---


### アドオンを無効化する

[1-5節](../chapter_01/05_Install_own_Add-on.md) を参考に有効化したアドオンを無効化すると、コンソールウィンドウに以下の文字列が出力されます。

```sh
サンプル3-3: アドオン「サンプル3-3」が無効化されました。
```


## ソースコードの解説

前節までに説明した内容については、説明を省きます。ソースコードにコメントを残していますので、必要に応じて参照してください。
本節では、タイマイベントを扱う処理と作業時間計測の処理に絞って説明します。


### タイマの登録

タイマイベントを扱うためには、タイマを登録する必要があります。

タイマの登録処理は、次に示す ```__handle_add()``` メソッドで行っています。

[import:"add_timer", unindent:"true"](../../sample_raw/src/chapter_03/sample_3_3.py)

タイマの登録は、```context.window_manager.event_timer_add()``` 関数で行っています。```context.window_manager.event_timer_add()``` 関数は次に示す引数を取り、戻り値としてタイマのハンドラを返します。戻り値として返されたハンドラはタイマの登録を解除する時に使用するため、インスタンス変数 ```timer``` に保存します。ここで、```timer``` はインスタンス変数でなければ正しく動作しないので注意が必要です。

|引数|値の意味|
|---|---|
|第1引数|タイマイベントを発生させる間隔を秒で指定|
|第2引数|タイマイベントを登録するウィンドウ|

本節のサンプルでは第1引数に ```0.1``` を指定することで、タイマイベントを0.1秒ごとに発生させています。第2引数には、作業時間の測定を開始した時に押したボタンが存在するウィンドウにタイマイベントを発生させたいため、```context.window``` を指定します。

最後にモーダルモードへ移行する処理を行っていますが、必ずしも ```__handle_add()``` メソッドで行う必要はありません。```__handle_add()``` メソッド自体が ```invoke()``` メソッドから呼び出されているので、[3-1節](01_Handle_Mouse_Click_Event.md) や [3-2節](02_Handle_Keyboard_Key_Event.md) と同様、```invoke()``` メソッドの処理内で ```context.window_manager.modal_handler_add()``` 関数を呼んでモーダルモードへ移行しても良いです。


### タイマの登録を解除

タイマを登録すると、登録を解除するまでタイマイベントを送り続けます。このため、タイマが不要になったら登録を解除する必要があります。

タイマの登録解除処理は、次に示す ```__handle_remove()``` メソッドで行っています。

[import:"remove_timer", unindent:"true"](../../sample_raw/src/chapter_03/sample_3_3.py)

タイマの登録解除は ```context.window_manager.event_timer_remove()``` 関数で行いますが、引数には ```context.window_manager.modal_handler_add()``` 関数の戻り値として返されたタイマのハンドラを渡す必要があります。本節のサンプルでは、タイマのハンドラを保存したインスタンス変数 ```timer``` を引数に渡しています。

登録解除後のタイマのハンドラは、測定を再開する時のために ```None``` を代入します。


### modalメソッド

[3-1節](01_Handle_Mouse_Click_Event.md) や [3-2節](02_Handle_Keyboard_Key_Event.md) と同様に ```modal()``` メソッドでは、*3Dビュー* エリアの画面更新と ```modal()``` メソッドの終了判定処理を行います。その後、オブジェクトの位置を更新します。

タイマイベントが発生すると、```modal()``` メソッドが呼ばれますが、[3-1節](01_Handle_Mouse_Click_Event.md) や [3-2節](02_Handle_Keyboard_Key_Event.md) で説明したように、```modal()``` メソッドはキーボードやマウスのイベントが発生した時にも呼ばれます。このためマウスやキーボードのイベントについて特別扱いしないと、タイマイベント発生時のみオブジェクトを移動する仕様を満たせなくなってしまいます。そこで次のようにして、発生したイベントがタイマイベントでない時に```{'PASS_THROUGH'}``` を返すことで、マウスやキーボードからのイベントが発生した時にオブジェクトが移動しないようにします。

[import:"handle_timer_event", unindent:"true"](../../sample_raw/src/chapter_03/sample_3_3.py)

続いて、終了ボタンが押された時にオブジェクトの移動を停止する処理を実行します。終了ボタンが押された時は、オブジェクトの移動を停止する以外にもオブジェクトを開始ボタンが押された時の初期位置に移動させる必要があります。

[import:"stop_moving_object", unindent:"true"](../../sample_raw/src/chapter_03/sample_3_3.py)


### オブジェクトの位置を更新する

タイマイベント発生時にオブジェクトの位置を更新する処理は、```__update_object_location()``` メソッドで行います。

[import:"update_object_location", unindent:"true"](../../sample_raw/src/chapter_03/sample_3_3.py)

オブジェクトの初期位置はインスタンス変数 ```orig_obj_loc``` の値に保存されているため、オブジェクトの初期位置に移動先の位置を相対座標で加えることでオブジェクトの位置を更新します。オブジェクトの位置は ```obj.location``` から参照・変更することができます。

本節のサンプルでは、タイマイベントが発生して ```__update_object_location()``` メソッドが呼び出されると ```self.count``` がカウントアップされます。これにより回転角がタイマイベント毎に増加するため、オブジェクトが初期位置を中心として半径 ```5.0``` 、各速度 ```3.0``` で回転します。


### invokeメソッド

オブジェクトの初期位置は、```invoke()``` メソッドの開始ボタンが押された時の処理の中で、インスタンス変数である ```orig_obj_loc``` にオブジェクトをキーとして保存されています。Blender上のオブジェクトには次のような型があります。本節のサンプルでは選択中のメッシュ型のオブジェクトを移動の対象としているため、```obj.select``` が ```True``` かつ ```obj.type == 'MESH'``` を満たすオブジェクトの位置のみを取得しています。

|型|意味|
|---|---|
|```MESH```|メッシュ|
|```CURVE```|カーブ|
|```SURFACE```|サーフェス|
|```META```|メタオブジェクト|
|```FONT```|テキストオブジェクト|
|```ARMATURE```|アーマチュア|
|```LATTICE```|ラティス|
|```EMPTY```|空のオブジェクト|
|```CAMERA```|カメラ|
|```LAMP```|ランプ|
|```SPEAKER```|スピーカー|

[import:"store_obj_loc", unindent:"true"](../../sample_raw/src/chapter_03/sample_3_3.py)


<div id="tips"></div>

上記のコードでは obj.location.copy() に示すように copy() メソッドを用いて、位置情報を示す Vector オブジェクトのコピーを作っています。Vector オブジェクトのコピーを作らないと位置情報の参照を持ち続けることになるため、初期位置情報として保存していたはずが \_\_update_object_location() メソッドで移動後の位置情報に書き換えられてしまい、オブジェクトの位置更新処理が正しく動作しません。


最後に、```__update_object_location()``` メソッドを呼び出してオブジェクトの位置を更新します。


### パネル表示/非表示切り替え

*3Dビュー* エリアのプロパティパネルに追加した *一定間隔でオブジェクトを移動* パネルは、```poll()``` クラスメソッドで表示する条件を絞っています。本節のサンプルでは最低でも1つのメッシュ型のオブジェクトが選択され、かつオブジェクトモードの時にパネルを表示しています。オブジェクトの型がメッシュ型かつ選択された状態であるかを判定する方法は先ほど書きました。そして、現在のオブジェクトが *オブジェクトモード* と *エディットモード* のどちらの状態にあるのかは ```obj.mode``` により取得することができるため、先ほどのパネル表示条件を満たしたことを判定するコードは次のようになります。

[import:"poll", unindent:"true"](../../sample_raw/src/chapter_03/sample_3_3.py)

なお、```obj.mode``` には次のような値が設定されます。オブジェクトが現在どのようなモードであるかを確認したい場合に利用することができます。

|値|モード|
|---|---|
|```OBJECT```|オブジェクトモード|
|```EDIT```|エディットモード|
|```SCULPT```|スカルプトモード|
|```VERTEX_PAINT```|頂点ペイント|
|```WEIGHT_PAINT```|ウェイトペイント|
|```TEXTURE_PAINT```|テクスチャペイント|
|```PARTICLE_EDIT```|パーティクル編集|
|```POSE```|ポーズモード|


<div id="tips"></div>

*オブジェクトモード* か *エディットモード* かを判定する方法としては、```bpy.context.mode``` を参照して ```'OBJECT'``` であることを確かめる方法もあります。また、*オブジェクトモード* 時のみパネルを表示したい場合は、[2-9節](../chapter_02/09_Control_Blender_UI_2.md) で示したパネルクラスのクラス変数 ```bl_context``` に ```objectmode``` を指定する方法があります。


## まとめ

タイマのイベントを扱う方法を説明しました。タイマを使うと指定した間隔でイベントを発生させることができるため、定期的に処理を実行するような機能を実現することができます。

[3-1節](01_Handle_Mouse_Click_Event.md) から本節まで3節にわたってイベントを扱う処理を説明しました。次節からは、Blenderが提供する少し特殊なモジュールを使ったアドオンを紹介します。


<div id="point"></div>

### ポイント

<div id="point_item"></div>

* タイマを登録することで、一定間隔でイベントを発生させることができる
* タイマの登録は ```context.window_manager.event_timer_add()``` 関数で行い、不要になったタイマは ```context.window_manager.event_timer_remove()``` 関数で登録を解除する
* タイマイベントが発生すると、```context.window_manager.modal_handler_add()``` の引数に指定したインスタンスの ```modal()``` メソッドが呼び出され、引数 ```event.type``` に ```TIMER``` が設定される
