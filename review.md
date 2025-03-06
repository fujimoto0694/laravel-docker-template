# Laravel Lesson レビュー①

## Todo一覧機能

### Todoモデルのallメソッドで実行しているSQLは何か
$todos = $todo->all();
全てのレコードを取得する意味を持つ。

### Todoモデルのallメソッドの返り値は何か
Illuminate、Database、Eloquent、Collectionクラスのインスタンス。

### 配列の代わりにCollectionクラスを使用するメリットは
メソッドチェーンなどを使え複雑な操作も簡潔にかけ可読性が向上するため。

### view関数の第1・第2引数の指定と何をしているか
return view('todo.index', ['todos' => $todos]);
第1引数には画面に表示したいHTMlを指定。todo.indexとはviews/todoの中にあるindex.blade.phpのことである。
第2引数には[blade内での変数名 => 代入したい値]を指定。ここではall()で全レコード取得した際に格納している$todosを代入している。

### index.blade.phpの$todos・$todoに代入されているものは何か
$todosは、TodoControllerクラスで実行された$todosが代入される。
$todoは、$todos内の複数のレコードが代入される。

## Todo作成機能

### Requestクラスのallメソッドは何をしているか
ファームから送信された値を連想配列として一括で取得している。

### fillメソッドは何をしているか
引数に指定した連想配列をモーダルに一括代入している。

### $fillableは何のために設定しているか
fill()でモーダルに代入可能なカラムを指定している。
代入可能なカラムを指定することで意図しないカラムの変更を防ぐことができる。

### saveメソッドで実行しているSQLは何か
saveメソッドは新しいレコードをデータベースに挿入、既存のレコードを更新する役割があるので、
ここのsaveメソッドは挿入のINSERT文が実行されている。

### redirect()->route()は何をしているか
todoが新規作成された際に一覧画面へリダイレクトしている。

## その他

### テーブル構成をマイグレーションファイルで管理するメリット
マイグレーションファイルをgitで共有できる為、開発者が同じテーブルを利用できる。
また、rollbackによってエラーが発生した際すぐに元に戻せたり、変更履歴がデータベースに残るメリットがある。

### マイグレーションファイルのup()、down()は何のコマンドを実行した時に呼び出されるのか
up()は「php artisan migrate」、artisanコマンドが呼び出されれた際に実行。
down()は「php artisan migrate:rollback」、rollbackコマンドが呼び出された際に実行。

### Seederクラスの役割は何か
runメソッド内に定義されたデータをINSERT文を用いてテーブルに挿入する役割。

### route関数の引数・返り値・使用するメリット
route関数の第一引数はURLパス、第二引数はURLにアクセスした際に実行するControllersのメソッドを指定。
返り値は、指定したメソッド内に定義されてるview()が返り値となる。
メリットは、URlに変更があった際route関数を使っていればweb.phpの変更のみで済む。


### @extends・@section・@yieldの関係性とbladeを分割するメリット
@extendsは、継承する親bladeの指定。
@sectionは、子Bladeの@section 〜 @endsectionで囲まれた部分を@yieldに挿入。
つまり@yieldは、@section 〜 @endsectionで囲まれた部分挿入先。
bladeを分割するメリットは、複数のbladeファイルで同じ記載箇所の修正があった際、同じ箇所を一つのファイルにまとめていれば修正箇所が一つで済むため。

### @csrfは何のための記述か
クロスサイトリクエストフォージェリの対策で、
トークンの照合を確認することで外部からのリクエストを受け付けない仕組み。

### {{ }}とは何の省略系か
bladeでphpを記述する際に使用されechoの省略系。
