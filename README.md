# Vue.js  ToDoListを作成しながら学習


## ファイルを構成する

- Vue.js-ToDoList-フォルダ内にindex.htmlファイルを作成する。
```
$ mkdir Vue.js-ToDoList-
$ touch index.html
```
- index.htmlファイルのレイアウトを構成する。

```
<!DOCTYPE html>
<html lang="ja">
<head>
  <meta charset="utf-8">
  <title>Vue.js ToDoList学習</title>
  <link rel="stylesheet" href="main.css">
</head>
<body>
  <div id="app"> (Vue.jsのアプリケーションを紐づける)

  </div>
  <script src="https://cdn.jsdelivr.net/npm/vue@2.6.12/dist/vue.js"></script> (Vue.jsのCDNを設定)
  <script src="main.js"></script>

</body>
</html>
```
- `main.css`ファイルと`main.js`ファイルを作成する。
- `main.js`ファイル内を構成する。
```
const app = new Vue ({
   el: "#app",
   data: {
       //リアクティブ要素にするためのデータを追加
   }
})
```
- データ表示の確認  
  
Vue.jsのアプリケーションを紐づけたdivタグの中に`{{ データの名前 }}`を使用
```

<body>
  <div id="app">
    {{ message }}
  </div>
  <script src="https://cdn.jsdelivr.net/npm/vue@2.6.12/dist/vue.js"></script>
  <script src="main.js"></script>

</body>

```

Vueインスタンスの中でdataプロパティを定義する。

```
var app = new Vue ({
   el: "#app"
   data: {
       message: "Hello World",
   }
});
```
ブラウザ上で確認する。

## データをバインディングする
`{{ message }}`に`v-model`ディレクテブを追加する(入力したデータとバインディングしたいので`type=text`とし、テキストボックスを追加)。
```

<body>
  <div id="app">
    <input type="text" v-model="message">
    {{ message }}
  </div>
  <script src="https://cdn.jsdelivr.net/npm/vue@2.6.12/dist/vue.js"></script>
  <script src="main.js"></script>
</body>

```
ブラウザ上で確認する。

## チェックボックスを追加する

input要素に `v-model="true"` であればチェックがつき、 `v-model="false"` であればチェックがはずれ
る。
```

<body>
  <div id="app">
    <input type="text" v-model="message">
    <input type="checkbox" v-model="isChecked">
    {{ message }} {{ isChecked }}
  </div>
  <script src="https://cdn.jsdelivr.net/npm/vue@2.6.12/dist/vue.js"></script>
  <script src="main.js"></script>

</body>

```
```
var app = new Vue ({
   el: "#app",
   data: {
       message: "Hello World",
       isChecked: true
   },
})
```
ブラウザ上で確認する。

## リストを追加する

Vue.jsのアプリケーションを紐づけたdivタグの中に`v-for`ディレクティブを使用。
データオプション内に特定の配列を作成し、`v-for`で指定する。
```

<body>
  <div id="app">
    <input type="text" v-model="message">
    <input type="checkbox" v-model="isChecked">
    {{ message }} {{ isChecked }}
    <ul>
      <li v-for="thing in things">{{ thing.title }}</li>
    </ul>
  </div>
  <script src="https://cdn.jsdelivr.net/npm/vue@2.6.12/dist/vue.js"></script>
  <script src="main.js"></script>

</body>

```

```
var app = new Vue ({   
   el: "#app",  
   data: {  
       message: "Hello World",  
       isChecked: true,  
       things: [  
        { title: 'やること1'},  
        { title: 'やること2'},  
        { title: 'やること3'},  
    ]  
   },  
})  
```
ブラウザ上で確認する。

## クリックイベントを追加する

ボタンをクリックする度に数が1ずつ増えていくイベントを追加してみる。  
Vue.jsのアプリケーションを紐づけたdivタグの中に`v-on:click`を使用する。  
`methods`オプションを作成し、その中で関数を定義する。  
データオプション内のデータは`this.データ名`で参照できる。  
```

<body>
  <div id="app">
    <input type="text" v-model="message">
    <input type="checkbox" v-model="isChecked">
    {{ message }} {{ isChecked }}
    <ul>
      <li v-for="thing in things">{{ thing.title }}</li>
    </ul>
    {{ counter }}
    <button v-on:click="add">add</button>
  </div>
  <script src="https://cdn.jsdelivr.net/npm/vue@2.6.12/dist/vue.js"></script>
  <script src="main.js"></script>

</body>

```

```
var app = new Vue ({
   el: "#app",
   data: {
       message: "Hello World",
       isChecked: true,
       things: [
        { title: 'やること1'},
        { title: 'やること2'},
        { title: 'やること3'},
        
       ],
       counter: 0
   },
   methods: {
       add: function(){
           this.counter++
       },
   },
})
```
ブラウザ上で動作確認する。

## ToDoListの作成

上記で確認した機能を組み合わせて実際にToDoListを作成してみる。

- ToDoリストを表示させる
```
<!DOCTYPE html>
<html lang="ja">
<head>
  <meta charset="utf-8">
  <title>Vue.js ToDoList学習</title>
  <link rel="stylesheet" href="main.css">
</head>
<body>
  <div id="app">
    <input type="text" v-model="message">
    <ul>
      <li v-for="thing in things">
        <label>
          <input type="checkbox" v-model="thing.isChecked"> {{ thing.title }}
        </label>
      </li>  
    </ul>
    <button v-on:click="add">add</button>
  </div>
  <script src="https://cdn.jsdelivr.net/npm/vue@2.6.12/dist/vue.js"></script>
  <script src="main.js"></script>

</body>
</html>
```
リストのプロパティ内には下記の2点を入れる。
- ToDoリストの内容
- チェックボックスによる確認
```
var app = new Vue ({
   el: "#app",
   data: {
       things: [
        { title: 'やること1', isChecked: false,},
        { title: 'やること2', isChecked: false,},
        { title: 'やること3', isChecked: true,},
       ],
       counter: 0
   },
   methods: {
       add: function(){
           this.counter++
       },
   },
})
```
ブラウザで確認する。

- ToDoリストに新しいToDo要素を追加する

テキストボックス内に新しいToDo要素を入力し、追加ボタンをクリックした際にToDoリストに追加されるようにする。

`<div id="app">` 内の　テキストボックス内の要素と`<button>`タグの中身を下記を修正する。
```

  <div id="app">
    <h1>To Do List</h1>
    <ul>
      <li v-for="thing in things">
        <label>
          <input type="checkbox" v-model="thing.isChecked"> {{ thing.title }}
        </label>
      </li>  
    </ul>
    <input type="text" v-model="newthings">
    <button v-on:click="add">追加</button>
  </div>
  
```

データ内に`newthings`を追加し`v-model`でバインディングする(入力した内容が追加されるようにしたいので値を空白に設定する)。  
追加ボタンを押したときにテキストボックスに入力された要素を既存の`thingリスト`に追加する関数を定義する(`v-on:click=関数名`でバインディング)

```
var app = new Vue ({
   el: "#app",
   data: {
       things: [
        { title: 'やること1', isChecked: false,},
        { title: 'やること2', isChecked: false,},
        { title: 'やること3', isChecked: true,},
       ],   
       newthings:"",
   },
   methods: {
       add: function(){
           this.things.push({
               title: this.newthings,
               isChecked: false,
           });
       },
   },
})
```
追加ボタンを押すとテキストボックス内に入力した文字が残ってしまうので残らないようにする。
`add`関数の最後にその処理を追加する。
```

   methods: {
       add: function(){
           this.things.push({
               title: this.newthings,
               isChecked: false,
           });
           this.newthings = "";
       },
   },

```

- 追加ボタンをEnterキーでクリックできるようにする

`<form @submit.prevent="add">`でテキストボックスタグとボタンタグを括る。  
formタグで関数`add`をバインディングしてるので、ボタンタグの中身は`type="submit`とする。
```

  <div id="app">
    <h1>To Do List</h1>
    <ul>
      <li v-for="thing in things">
        <label>
          <input type="checkbox" v-model="thing.isChecked"> {{ thing.title }}
        </label>
      </li>  
    </ul>
    <form @submit.prevent="add">
      <input type="text" v-model="newthings">
      <button type="submit">追加</button>
    </form>
  </div>
  
```

 - 終了したToDoをリストから削除する

削除していかないとリストが溢れて見にくくなってしまうため、リストから終わったToDoを削除する機能を追加する。  
新しく削除ボタンを追加し、クリックした時にテキストボックスのチェック済み項目(`things`配列内のオブジェクト)を更新する関数を`methods`オプションに追加する。

```

  <div id="app">
    <h1>To Do List</h1>
    <ul>
      <li v-for="thing in things">
        <label>
          <input type="checkbox" v-model="thing.isChecked"> {{ thing.title }}
        </label>
      </li>  
    </ul>
    <form @submit.prevent="add">
      <input type="text" v-model="newthings">
      <button type="submit">追加</button>
    </form>
    <button v-on:click="delete">削除</button>
  </div>
  
```

関数内では`filter`メソッドを使用する。
```

   methods: {
       add: function(){
           this.things.push({
               title: this.newthings,
               isChecked: false,
           });
           this.newthings = "";
       },
       deleteTodo: function(){
           this.things = this.things.filter(function(thing){
               return thing.isChecked === false;
           });
       },
   },
})
```
ブラウザ上で確認する。

- テキストボックス内が空欄の場合、リストに追加できないようにする。

`add`関数内に`if`文を追加する。
```
var app = new Vue ({
   
   methods: {
       add: function(){
           if(this.newthings == "")return;
           this.things.push({
               title: this.newthings,
               isChecked: false,
           });
           this.newthings = "";
       },
       deleteTodo: function(){
           this.things = this.things.filter(function(thing){
               return thing.isChecked === false;
           });
       },
   },
})
```

- チェックしたリストに打ち消し線を引く

label要素にclass属性を設定し、打ち消し戦が入るようにする。  
head内要素に打ち消し線を表示するスタイルを追加する。
```
<!DOCTYPE html>
<html lang="ja">
<head>
  <meta charset="utf-8">
  <title>Vue.js ToDoList学習</title>
  <link rel="stylesheet" href="main.css">
  <style>
    .done { text-decoration: line-through; }
  </style>
</head>
<body>
  <div id="app">
    <h1>To Do List</h1>
    <ul>
      <li v-for="thing in things">
        <label v-bind:class="{ done: thing.isChecked }">
          <input type="checkbox" v-model="thing.isChecked"> {{ thing.title }}
        </label>
      </li>  
    </ul>
    <form @submit.prevent="add">
      <input type="text" v-model="newthings">
      <button type="submit">追加</button>
    </form>
      <button v-on:click="deleteTodo">削除</button>
  </div>
  <script src="https://cdn.jsdelivr.net/npm/vue@2.6.12/dist/vue.js"></script>
  <script src="main.js"></script>

</body>
</html>
```

- ToDoリストに日付を表示する

`<div id="app">` 内に`{{ 関数名 }}`を指定。  
```
<body>
  <div id="app">
    <h1>To Do List</h1>
    <p>{{setDate}}</p>
    <ul>
      <li v-for="thing in things">
        <label v-bind:class="{ done: thing.isChecked }">
          <input type="checkbox" v-model="thing.isChecked"> {{ thing.title }}
        </label>
```
date内に`computed`プロパティを作成し、日付をとる関数を定義する。
```
computed: {
    setDate: function() {
        hiduke = new Date();
        year = hiduke.getFullYear();
        month = hiduke.getMonth()+1;
        day = hiduke.getDate();
        return this.transfer_data = year + '/' + month + '/' + day ;
        } 
   }
```

- リストを削除する際にアラートを表示して確認する。

`deleteTodo`関数内に`confirm`メソッドを追加する。
```
deleteTodo: function(){
           result = confirm("本当に終わりましたか？");
           if(result) {
              this.things = this.things.filter(function(thing){
                  return thing.isChecked === false;
              })
           }else{

           }
       },
```

- コンパイル前の表示を隠す

コンパイルをする際にマスタッシュ構文が一瞬表示されるのを非表示にする。
`v-cloak`ディレクティブを使う。
`div`タグにv-cloakを追加する。
```
<div id="app" v-cloak>
```
CSS内でv-cloakを指定し、`display:none`を付与する。
```
[v-cloak]{
    display:none;
  }
```

- テキストボックス入力時に誤った空白(space)を無くしてあげる。

フォーム入力バインディングの修飾子`.trim`を`v-model`の後に追記する。
```
    <form @submit.prevent="add">
      <input type="text" v-model.trim="newthings">
      <button type="submit">追加</button>
    </form>
```

- リストを初期化した状態にする。

既存のコードではブラウザを立ち上げた時にデフォルトでリストが表示されてしまっていたため、その点を訂正。
`date`オプション内の中身の初期値を設定。変更点はここのみ。
```
data: {
       title: "",
       things: []
   },
```


- ToDoリストが何もない場合、デフォルトで文字を表示させておく

ToDoを全て終えた、若しくはまだ1つもToDoを追加していない場合、ブラウザ上に現在やることはありませんと表示させたい。    
`if`文を使って`things`ないの要素がないときは、表示、あるときは非表示と設定出来れば良い。  
`list`要素内に`v-if``v-else`で条件を定義。 
 if条件でリストの`length`の数によって条件分岐をさせるため、`things.length <= 0`を条件式とし、true(v-if)の場合は表示させたい文字を渡し、false(v-if)の場合は空欄を渡す。  

 ```
<ul>
      <li v-if="things.length <= 0">現在やることはありません</li>
      <li v-else></li>
      <li v-for="thing in things">
        <label v-bind:class="{ done: thing.isChecked }">
          <input type="checkbox" v-model="thing.isChecked"> {{ thing.title }}
        </label>
      </li>  
    </ul>
 ```
- コンパイルでデータがリセットされるのを防ぐ

コンパイルするとリストがリセットされてしまうので、データをブラウザに保存し、初期表示の際に利用する。    
データをブラウザに保存する際は、`localStorage`に`things`配列を保存する。  
methodsオプションにその関数を定義する。  
配列のままでは入れることができないので、文字列に変換する`JSON.stringify`を使用する。  
`localStorage.setItem("配列名"JSON.stringify(this.値))`で実装。  
```
saveList: function(){
  localStorage.setItem('things', JSON.stringify(this.things));
},
```

項目を追加、削除した際にブラウザに保存するために、`add`関数と`deleteTodo`関数内の最後に`saveList`を呼び出す。  
```
add: function(){
           if(this.newthings == "")return;
           this.things.push({
               title: this.newthings,
               isChecked: false,
           });
           this.newthings = "";
           this.saveList();
       },
```
```
deleteTodo: function(){
           result = confirm("本当に終わりましたか？");
           if(result) {
              this.things = this.things.filter(function(thing){
                  return thing.isChecked === false;
              })
           }else{

           };
           this.saveList();
       },
```

チェックボックスを操作した際にも配列の中身は変わるので、そこでも関数を呼び出す。  
```
<ul>
      <li v-if="things.length <= 0">現在やることはありません</li>
      <li v-else></li>
      <li v-for="thing in things">
        <label v-bind:class="{ done: thing.isChecked }">
          <input type="checkbox" v-model="thing.isChecked" v-on:change="saveList"> {{ thing.title }}
        </label>
      </li>  
    </ul>
```

保存の確認はデベロッパーツールの `application`> `Storage > localStorage > file://` と降り、選択したときに右側に `things` が保存されているのが見える。

- データをブラウザから読み出す

dataオプション内の配列thingsにブラウザ内のデータを持ってくる。
ブラウザ内のデータは文字列なので、`JSON.parse`で配列に直す。
ブラウザにデータが無い場合、if文で条件分岐し空の配列を入れる。
```
loadList: function(){
           this.things=JSON.parse(localStorage.getItem('things'));
           if(!this.things){
               this.things=[];
           }
```

初期表示時に動く処理は `mounted` オプションで指定できる。
`methods`オプション内に下記を追加。
```
mounted: function(){
           this.loadList();
       }
```

- マスタッシュの代わりにディレクティブを使う

 マスタッシュ構文の代わりにディレクテブ`v-text`ディレクテブを使ってデータバインディングする。
 ```
<div id="app" v-cloak>
    <h1>To Do List</h1>
    <p v-text="setDate"></p>
 ```

 - placeholderの追加

```
<form @submit.prevent="add">
      <input type="text" v-model.trim="newthings" placeholder="ToDoを入力して下さい">
      <button type="submit">追加</button>
    </form>
```

- v-bindを省略形で記述する

```
<li v-for="thing in things">
        <label :class="{ done: thing.isChecked }">
          <input type="checkbox" v-model="thing.isChecked" v-on:change="saveList">{{ thing.title }}
        </label>
      </li>  
```
