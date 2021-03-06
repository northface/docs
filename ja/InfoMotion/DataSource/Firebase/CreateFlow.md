---
lastUpdated: 2018-08-09
---

# フローの作成

Firebase の準備ができたのでデータをプッシュするフローを作成します。
enebular のプロジェクトの右下の +ボタンをクリックし、新しいフローを作成します。

![CreateFlow-flowList](./../../../../img/InfoMotion/DataSource/firebase/CreateFlow-flowList.png)


任意の名前を付けて [Continue] をクリックします。

![CreateFlow-createFlow](./../../../../img/InfoMotion/DataSource/firebase/CreateFlow-createFlow.png)


[Edit Flow] をクリックしてフローエディターを開きます。

![CreateFlow-editFlow](./../../../../img/InfoMotion/DataSource/firebase/CreateFlow-editFlow.png)


下記のノードを配置し、下記の画像のようなフローを作成してください。

* inject ノード
* function ノード
* firebase modify ノード
* debug ノード

(もし、Firebase のノードが存在してなかったら、 `node-red-contrib-firebase` を admin タブよりインストールしてください)

![CreateFlow-flow](./../../../../img/InfoMotion/DataSource/firebase/CreateFlow-flow.png)


次に inject ノード(表示は timestamp )のモーダル画面を表示します。

 `repeat` を [interval] とし、every [10] seconds に設定します。
 [Done] をクリックして、モーダル画面を閉じます。

![CreateFlow-injectNode](./../../../../img/InfoMotion/DataSource/firebase/CreateFlow-injectNode.png)


function ノードをダブルクリックして `edit function node` のモーダル画面を表示してください。
下記スクリプトをコピーして Function に貼り付けます。

![CreateFlow-functionNode](./../../../../img/InfoMotion/DataSource/firebase/CreateFlow-functionNode.png)


```javascript
var data = {
        timestamp: Date.now(),
        value:{
            category:['A','B','C','D'][Math.floor(Math.random()*4)],
            value: Math.floor(Math.random()*10),
            created:Date.now()
        }
      }
      
msg.payload = data;
return msg;
```


次にfirebase ノードのモーダル画面を表示します。
鉛筆のアイコンをクリックして、`Edit firebase config node` のモーダル画面を表示します。

`Firebase` には先ほど作成した Firebase プロジェクトの ID を入力してください。
`Auth Type` は [None] を選択します。設定が終わったら [Add] をクリックして保存します。

![CreateFlow-firebaseConfigNode](./../../../../img/InfoMotion/DataSource/firebase/CreateFlow-firebaseConfigNode.png)


`Child path`には「test」 を入力し、`Method` は [push] を選択、`value` は「msg.payload」のままにし、 [Done] をクリックします。

![CreateFlow-firebaseNode](./../../../../img/InfoMotion/DataSource/firebase/CreateFlow-firebaseNode.png)


全てのノードの準備ができたので、 [Deploy] を押してノードを実行します。

フローの実行ログをエディター右部のデバッグタブより閲覧できます。
下記のようなログが表示され、正しくフローが実行されていることを確認してください。

![CreateFlow-debugLog](./../../../../img/InfoMotion/DataSource/firebase/CreateFlow-debugLog.png)


次に Firebase のページで先ほど作ったアプリからデータにデータが追加されているか確認します。

![CreateFlow-firebaseProjectDatabase-ja](./../../../../img/InfoMotion/DataSource/firebase/CreateFlow-firebaseProjectDatabase-ja.png)