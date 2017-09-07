# SkyWay iOS SDK 差分情報

## SKWPeer

### メソッド

#### 新規追加

##### `- (SKWRoom*)joinRoomWithName:(NSString*)roomName options:(SKWRoomOption*)option`

`SKWRoomOption` に従って `SKWMeshRoom` または `SKWSFURoom` のインスタンスを生成します。`SKWMeshRoom` および `SKWSFURoom` については後述します説明を参照してください。

## SKWCallOption

### プロパティ

下記のプロパティが増えています。

プロパティ名   | 型
-------------- | ------
label          | NSString*
videoBandwidth | NSUInteger
audioBandwidth | NSUInteger
videoCodec     | NSString*
audioCodec     | NSString*

## SKWConnectOption

### プロパティ

#### 仕様変更

##### `serialization`

`SKW_SERIALIZATION_BINARY` が `SKW_SERIALIZATION_BINARY_UTF8` と同じ扱いになり、js-binarypack フォーマットでシリアライズします。

##### `reliable`

デフォルト `YES` となり、libwebrtcの制約で `NO` は選択できなくなります。

## SKWDataConnection / SKWMediaConnection 共通

### プロパティ

#### 仕様変更

##### `peerConnection`

`RTCPeerConnection` は型が `id` に変更になり、このプロパティは常に `nil` となります。

### メソッド

#### 仕様変更

##### `- (void)getPeerConnectionState:(BOOL)bOutputDebug callback:(void(^)(NSArray*))callback`

コネクションステータスが取得できなくなりました。
このメソッドは[旧SDKのドキュメント](http://nttcom.github.io/skyway/docs/#iOS)に記載はありません。

## SKWDataConnection

### プロパティ

#### 仕様変更

##### `dataChannel`

型が `id` となり常に `nil` となります。

## SKWMediaConnection

### メソッド

#### 新規追加

##### `- (void)answer:(SKWMediaStream*)stream options:(SKWAnswerOption*)options`

`-answer:` に `SKWAnswerOption` を指定できるようになりました。

##### - (void)replaceStream:(SKWMediaStream* __nullable)newStream;

送信している MediaStream を更新します。受信のみモードから双方向に切り替えることも出来ます。

## SKWAnswerOption

新規メソッド `-answer:options:` のオプション指定クラスです。

## SKWMeshRoom

フルメッシュルームを表す新規クラスです。

### メソッド

#### 新規追加

##### - (void)replaceStream:(SKWMediaStream* __nullable)newStream;

送信している MediaStream を更新します。受信のみモードから双方向に切り替えることも出来ます。

## SKWSFURoom

SFU ルームを表す新規クラスです。

### メソッド

#### 新規追加

##### - (void)replaceStream:(SKWMediaStream* __nullable)newStream;

送信している MediaStream を更新します。受信のみモードから双方向に切り替えることも出来ます。

## SKWRoomEventEnum

`SKWMeshRoom` インスタンス、 `SKWSFURoom` インスタンスで発生するイベントの列挙子です。

## SKWRoomOption

新規メソッド `- joinRoomWithName:options:` のオプション指定クラスです。

## SKWMediaStream

### プロパティ

下記のプロパティが増えています。

プロパティ名 | 型        | 備考
------------ | --------- | -----
label        | NSString* | |
peerId       | NSString* | `SKWNavigator -getUserMedia` で生成したメディアストリームでは空文字列が返されます。

### メソッド

#### 新規追加

##### `- (void)addVideoRenderer:(SKWVideo*)renderer track:(NSUInteger)trackNo`

[旧SDKのドキュメント](http://nttcom.github.io/skyway/docs/#iOS) の [SKWVideo -addSrc:track:](http://nttcom.github.io/skyway/docs/#iOS-skwvideo-addsrc) に相当するメソッドです。

##### `- (void)removeVideoRenderer:(SKWVideo*)renderer track:(NSUInteger)trackNo`

[旧SDKのドキュメント](http://nttcom.github.io/skyway/docs/#iOS) の [SKWVideo -removeSrc:track:](http://nttcom.github.io/skyway/docs/#iOS-skwvideo-removesrc) に相当するメソッドです。`-addVideoRenderer:track:` で割り当てた `SKWVideo` インスタンスを取り除きます。

## SKWPeerError

### プロパティ

下記のプロパティが増えています。

プロパティ名 | 型
------------ | ---------
typeString   | NSString*

サーバから返される ERROR メッセージの `type` をそのまま格納しています。
