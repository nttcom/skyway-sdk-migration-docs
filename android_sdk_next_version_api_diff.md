# SkyWay Android SDK 次期バージョン API 差分

## Peer

### プロパティ

下記のプロパティがメソッドに変更になりました。

変更前           | 変更後
---------------- | ----------------
`identity`       | `identity()`
`isDisconnected` | `isDisconnected()`
`isDestroyed`    | `isDestroyed()`

### メソッド

#### 新規追加

##### `public Room joinRoom(String roomName, RoomOption option)`

`RoomOption` に従って `MeshRoom` または `SFURoom` のインスタンスを生成します。`MeshRoom` および `SFURoom` については後述します説明を参照してください。

## CallOption

### プロパティ

下記のプロパティが増えています。

プロパティ名   | 型
-------------- | ------
label          | String
videoBandwidth | int
audioBandwidth | int
videoCodec     | String
audioCodec     | String

## ConnectOption

### プロパティ

#### 仕様変更

##### `serialization`

`BINARY` が `BINARY_UTF8` と同じ扱いになり、js-binarypack フォーマットでシリアライズします。

##### `reliable`

デフォルト `true` となり、libwebrtcの制約で `false` は選択できなくなります。

## MediaConnection / DataConnection 共通

### プロパティ

下記のプロパティが getter メソッドに変更になりました。

変更前           | 変更後
---------------- | ----------------
connectionId     | connectionId()
isOpen           | isOpen()
peer             | peer()
type             | type()
label            | label()
reliable         | reliable()
serialization    | serialization()
metadata         | metadata()
provider         | provider()
peerConnection   | peerConnection()

`connectionId` 、 `provider` は[現在のドキュメント](http://nttcom.github.io/skyway/docs/#Android)に記載はありません。
`peerConnection` は返される型が `Object` に変更になり、この getter メソッドを呼び出しても常に `null` が返されます。

## DataConnection

### プロパティ

`dataChannel` は削除されました。

### メソッド

#### 仕様変更

##### `public void getPeerConnectionState(OnCallback listener)`

コネクションステータスが取得できなくなりました。
このメソッドは[現在のドキュメント](http://nttcom.github.io/skyway/docs/#Android)に記載はありません。

## MediaConnection

### メソッド

#### 仕様変更

##### `public void getPeerConnectionState(OnCallback listener)`

コネクションステータスが取得できなくなりました。
このメソッドは[現在のドキュメント](http://nttcom.github.io/skyway/docs/#Android)に記載はありません。

#### 新規追加

##### `public void answer(MediaStream stream, AnswerOption option)`

`answer()` に `AnswerOption` を指定できるようになりました。

##### `public void replaceStream(MediaStream stream)`

送信している MediaStream を更新します。受信のみモードから双方向に切り替えることも出来ます。

## AnswerOption

新規メソッド `MediaConnection#answer(MediaStream, AnswerOption)` のオプション指定クラスです。

## MeshRoom

フルメッシュルームを表す新規クラスです。

### メソッド

##### 新規追加

##### `public void replaceStream(MediaStream stream)`

送信している MediaStream を更新します。受信のみモードから双方向に切り替えることも出来ます。

## Room.MeshRoomEventEnum

`MeshRoom` インスタンスで発生するイベントの列挙子です。

## SFURoom

SFU ルームを表す新規クラスです。

### メソッド

##### 新規追加

##### `public void replaceStream(MediaStream stream)`

送信している MediaStream を更新します。受信のみモードから双方向に切り替えることも出来ます。

## Room.SFURoomEventEnum

`SFURoom` インスタンスで発生するイベントの列挙子です。

## RoomOption

新規メソッド `Peer#joinRoom(String, RoomOption)` のオプション指定クラスです。

## OnCallback2

`Room.RoomEventEnum` イベントの中に返される値が二つになるものが増えたため、`OnCallback` を継承した新規インターフェイスです。

## MediaStream

### プロパティ

下記のプロパティが増えています。

プロパティ名 | 型     | 備考
------------ | ------ | -----
getLabel()   | String | |
getPeerId()  | String | `Navigator#getUserMedia()` で生成したメディアストリームでは空文字列が返されます。

### メソッド

#### 新規追加

##### `public void addVideoRenderer(Canvas canvas, int videoTrackNumber)`

[現在のドキュメント](http://nttcom.github.io/skyway/docs/#Android) の [Canvas#addSrc()](http://nttcom.github.io/skyway/docs/#Android-canvas-addsrc) に相当するメソッドです。

##### `public void removeVideoRenderer(Canvas canvas, int videoTrackNumber)`

[現在のドキュメント](http://nttcom.github.io/skyway/docs/#Android) の [Canvas#removeSrc()](http://nttcom.github.io/skyway/docs/#Android-canvas-removesrc) に相当するメソッドです。`addVideoRenderer()` で割り当てた `Canvas` インスタンスを取り除きます。

## PeerError

### プロパティ

下記のプロパティが増えています。

プロパティ名 | 型
------------ | ------
typeString   | String

サーバから返される ERROR メッセージの `type` をそのまま格納しています。
