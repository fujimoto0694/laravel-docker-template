# Laravel Lesson レビュー②

## Todo編集機能

### @method('PUT')を記述した行に何が出力されているか
<input type="hidden" name="_method" value="PUT">
上記のinputタグが生成される。

### findメソッドの引数に指定しているIDは何のIDか
ルート定義で指定されたルートパラメータにあたる。
編集機能の場合、index.bladeの詳細で定義されてるrouteの第二引数から来ている。

### findメソッドで実行しているSQLは何か
findメソッドは引数部分のデータ取得になるのでSQLはSELECT文になる。

### findメソッドで取得できる値は何か
指定されたルートパラメータの全レコード。

### saveメソッドは何を基準にINSERTとUPDATEを切り替えているのか
新規でモデルが作成される場合INSERTが実行され、
既にモデルがデータベースに保存されている場合UPDATEが実行される。

## Todo論理削除

### traitとclassの違いとは
classは1つのclassに対し1つのclassしか継承できないが、traitは1つのclassに対し複数のtraitを継承できる。
classはインスタンス化できるがtraitはできない。

### traitを使用するメリットとは
1つのclassに複数の機能が追加できる。
コードの再利用が可能になるので可読性や保守性が向上する。

## その他

### TodoControllerクラスのコンストラクタはどのタイミングで実行されるか
Todoクラスがインスタンス化した瞬間にコンストラクタは実行される。

### RequestクラスからFormRequestクラスに変更した理由
入力内容をバリデーションするため。

### $errorsのhasメソッドの引数・返り値は何か
hasメソッドの引数はrulesメソッドで定義したバリデーションエラー。

### $errorsのfirstメソッドの引数・返り値は何か
firstメソッドの引数はmessagesメソッドで定義したエラーメッセージ。

### フレームワークとは何か
アプリ等の開発に必要な処理が予め定義されてる枠組みのこと。

### MVCはどういったアーキテクチャか
アプリケーションをmodel、view、controllerに分けて構成すること。

### ORMとは何か、またLaravelが使用しているORMは何か
LaravelのORMはEloquentと呼ばれており、classとtableを関連付けることでSQLを使用せずともDBの操作を可能にしている。

### composer.json, composer.lockとは何か
composer.jsonはプロジェクトが依存しているパッケージやライブラリが定義されているファイル。
composer.lockはプロジェクトでインストールされたパッケージのバージョン情報を記録したファイル。

### composerでインストールしたパッケージ（ライブラリ）はどのディレクトリに格納されるのか
vendorファイルに格納される。
