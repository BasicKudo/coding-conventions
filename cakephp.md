# CakePHP プログラミングガイド

ここではCakePHPを使ったシステム開発におけるプログラミングガイドを示します。

## システム構成

- PHP5.3〜
- CakePHP2.x系
- TwitterBootstrap
- CakePHP Plugin / TwitterBootstrap
- CakePHP Plugin / DebugKit
- PHPUnit

## 命名規約

テーブル名・クラス名などの命名は、CakePHPの規約に従ってください。従って、以下の様な名前になります。

|名前|説明|
| ---- | ---- |
|テーブル名|すべて小文字の複数形。複数の単語はアンダースコアでつなげる|
|コントローラー ファイル名|キャメルケースの複数形 + Controller.php（例 : PostsController.php）|
|コントローラー クラス名|キャメルケースの複数形 + Controller（例 : PostsController）|
|モデル ファイル名|キャメルケースの単数形 + .php（例 : Post.php）|
|モデル クラス名|キャメルケースの単数形（例 : Post）|
|ビュー ディレクトリ名|キャメルケースの複数形。コントローラー名からControllerという文字を省略したものと同じ。（例 : Posts）|
|ビュー ファイル名|すべて小文字の単数形 + .ctp。アクション名と同じ（例 : index.ctp）|

## Skinny Controller, Fat Model

コントローラーにビジネスロジックを置いたり、モデルから取得したデータを操作したりすると、あっという間にコントローラーがコードで溢れかえってしまいます。

後から見返した時に、インプット／アウトプットの流れが置いにくくなり、メンテナンスできない状態になりがちです。

ビジネスロジック・データ操作は、モデルに置いて、コントローラーは小さくシンプルに保つようにしましょう。

## メソッドは小さく

一つのメソッドには、一つの役割だけ与えるようにしましょう。さまざまなオプションを持つメソッドは、バグの原因になりがちです。

## アソシエーション／DB外部キーは標準で使用しない

CakePHPのアソシエーションは非常に強力で便利ですが、パフォーマンスを犠牲にしてしまう場面が多くあります。そのため、標準では設定せずに、必要な場面でアソシエーションの定義を行ってください。

また、開発時に実際に実行されるSQLを確認し、パフォーマンスに問題がないか気をつけてください。

## データトランザクション

データベースの更新を行う際には、トランザクションを実行してください。下記は、HogeコントローラからHogeモデルのトランザクションを実行している例です。

実際にはモデル自身でトランザクションを実行するケースが多いので、Transactionモデルを使わなくても自身を参照することで実行可能です。

### AppModel.php

```php
class AppModel extends Model {
	function begin() {
		$db =& ConnectionManager::getDataSource($this->useDbConfig);
		$db->begin($this);
	}

	function commit() {
		$db =& ConnectionManager::getDataSource($this->useDbConfig);
		$db->commit($this);
	}

	function rollback() {
		$db =& ConnectionManager::getDataSource($this->useDbConfig);
		$db->rollback($this);
	}
}
```

### Transaction.php

```php
class Transaction extends AppModel {
	public $name = 'Transaction';
}

```

### HogeController.php

```php
$this->Transaction->begin();
try {
	$this->save($data);
	$this->Transaction->commit();
} catch (Exception $e) {
	$this->Transaction->rollback();
}
```
