# NUnit
- .NET Core環境のテストフレームワーク
- テストエクスプローラーを用いてテストを行う
- 必要なパッケージ
  - Microsoft.NET.Test.Sdk
  - NUnit
  - NUnit Test Adapter

# NUnitの構成
- テストケース
  - 対象メソッドを呼び出しテストをする
- テストクラス
  - テストケースの集合
- テストスイート
  - テストエクスプローラーでテストプログラムを一度に実行することができる

# テストエクスプローラー
- テストプログラムを起動し，結果を表示する
- テスト成功でグリーン，失敗でレッドを表示
- レッド・グリーンテストとも

# テストクラスの作成場所
- 作成するアプリケーションの内容や規模などで異なる
  - ターゲットとテストクラスの名前空間を分ける
  - プロジェクトを分ける
  - 同一名前空間に作成する

# テストクラスの作成
- テストクラス作成基本ルール
  - ターゲットに対してテストクラスを一つ作成する
  - テスト項目やターゲットのメソッドが大量にあり，テストクラスが巨大になる場合は分割を検討する
- テストクラス作成の基本
  - テストクラス名には推奨される命名規則がある
    - `[テスト対象クラス名] + Test`
    - テストクラスが複数の場合は連番一桁を追加
  - NUnitの機能を利用できるように
    - `using NUnit.Framework`を追加
  - テストクラスであることを表す`[TestFixture]`属性をテストクラスに付与

# テストメソッドの作成
- テストメソッド作成基本ルール
  - テストケース一つに対して一つのテストメソッド
  - 一つのテストメソッドで一つの処理結果が判別できるようにする
  - テストメソッドを実行した結果は必ずアサーションメソッドを使って評価
  - テスト対象であることを表す`[Test]`属性をメソッドに付与
- テストメソッド作成の基本
  - `test + [テスト対象メソッド名] + _ + [テスト内容の説明]`
  - 引数は無し
  - 戻り値はvoid
- テストメソッド作成の手順
  - テストするクラスをインスタンス化する(staticの場合は不要)
  - 対象メソッドを呼び出す
  - 呼び出し結果を評価メソッドで評価する
- テストするメソッドの使用を理解していることが大前提
- 評価の仕方はメソッドの処理内容や引数，戻り値の内容により異なる

# アサーション(評価メソッド)の種類
- Assertクラスが用意している`That()`メソッドに制約クラスが提供する機能を用いて評価する

| メソッド                   | 機能                                                                                                           |
| -------------------------- | -------------------------------------------------------------------------------------------------------------- |
| `That(actual, constraint)` | 引数actualにはメソッド実行結果やテストしたいメソッドを指定する<br>引数constraintには期待する値や状態を指定する |

- 制約(constraint)クラス

| クラス | 機能                                             |
| ------ | ------------------------------------------------ |
| Is     | 数値やオブジェクトの評価機能を提供する           |
| Has    | コレクションの値の評価機能を提供する             |
| Does   | 文字列などのオブジェクトを評価する機能を提供する |
| Throws | 例外に関する評価機能を提供する                   |

# `[TestCase]`属性を利用したテストケースの記述
- 値の比較による評価の場合に利用する
- 属性にはターゲットメソッドの引数値や戻り値を指定することで，評価メソッドの記述を省略できる
- `[TestCase]`属性を利用した場合は`[Test]`属性の記述は不要

