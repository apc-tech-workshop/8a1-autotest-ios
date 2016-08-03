class:middle, center, inverse
# iOSでの自動テスト

APCommunications

---

# agenda

1. 自己紹介
1. テストについて
  - カテゴリ
  - 種類
  - 着手時期
1. 自動テストについて
  - ５０回連続操作
  - 効果的なテストパターン
1. テストケースについて
  - ターゲット追加
  - 部品へマーカーを設定
  - テストケース作成
  - テストケース生成
1. まとめ


???

- 今日のサマリーは
- テストって何やるのについてサラッと
- 自動化するのはどんな時かをサラッと
- 具体的にiOS/Swiftでテスケースの作り方を説明
- いたします

---

# 自己紹介

- 最近になってiOS Swiftし始めた（１ヶ月もない）
- プロマネとして自動UIテストをススメる立場
- 自分で書いてみたら意外と簡単だった
- 具体的な書き方が分からなくても、ヒントはXcodeがくれる事が分かった
- **序盤だけでも共有したい**

![:style height:60%](face.png)

???

- ハイ。
- 自己紹介ですが、
- 最近になってiOS Swiftを始めた伊藤です。
- バリバリのiOSプログラマという訳ではありません。
- プロジェクトでテストの自動化を進める立場にありました。
- 実際に自分で書いてみると意外と簡単だったので、
- これから自動テストを始めようという人に共有したいと思いました。


---
class: middle, center, inverse
layout: true
---
# テストについて

???

- まずは、テストについて良くわからない方のために
- サラッとご説明致します

---

layout: true
テストについて
---

# カテゴリ

- 単体テスト
- UIテスト
- インテグレーションテスト

???
- テストには、
- ロジック確認の単体テスト
- 部分シナリオでのUIテスト
- end to endのシナリオでのインテグレーションテスト
- があります。

---

layout: true
テストについて
---

# カテゴリ

- 単体テスト
- **UIテスト**
- インテグレーションテスト

???

- 今回は、部分シナリオのUIテストについて話します。

---
layout: true
テストについて
---

# 種類

- 確認
  - 正常系、異常系
  - インテグレーションテスト
- 反復
  - 正常系、異常系
- 耐久
  - OutOfMemory
  - 整合性

???

- そして、
- テストの種類には
- 実装の確認
- 冪等性やデグレ確認の反復
- 耐久性確認
- があります。

---
layout: true
テストについて
---

# 種類

- 確認
  - 正常系、異常系
  - インテグレーションテスト
- 反復 ***Oh! 苦行!!***
  - 正常系、異常系
- 耐久 ***Oh! 苦行!!***
  - OutOfMemory
  - 整合性

???

- 中でも、
- 反復と耐久は人間には苦行です

---
layout: true
テストについて
---

# 着手時期

画面部品の状況変化によって、確認したい内容の変化

1. ＜序盤＞
  - 状況：画面部品が揃わない
  - 確認：状態変化の妥当性

???

- 次に、
- 画面部品の状況変化と
- そのシーンで確認したい要素について、ですが
- 序盤は、部品の品質を確認をしたいです
- 中盤は、部品同士の整合性を確認したいです
- 終盤は、リサイクルの影響を確認したいです

--
1. ＜中盤＞
  - 状況：画面部品が揃いきった
  - 確認：反復操作への耐久性

--
1. ＜終盤＞
  - 状況：画面部品の再利用の機会が増えた
  - 確認：既存部品への影響度


---
layout: true
テストについて
---

# 着手時期

画面部品の状況変化によって、確認したい内容の変化

1. ＜序盤＞
  - 状況：画面部品が揃わない
  - 確認：状態変化の妥当性
1. **＜中盤＞**
  - **状況：画面部品が揃いきった**
  - **確認：反復操作への耐久性**
1. ＜終盤＞
  - 状況：画面部品の再利用の機会が増えた
  - 確認：既存部品への影響度

???

- 今回は、先程苦行だと言い表した
- 中盤の反復と耐久から自動テストを実施し始めるといいかなと思いました

---
class: middle, center, inverse
layout: true
---
# 自動テストについて

???

- では、その自動テストについてご説明いたします。

---

layout: true
自動テストについて
---

# ５０回連続操作して
# OutOfMemory
# の発生可否を確認する

???

- 例えば、耐久テストとして、
- 同じ操作を繰り返して、メモリ解放が適切か
- 確認するものが有ります。

---
layout: true
自動テストについて ５０回連続操作
---

## 人力

- １操作４秒
    - ５０操作２００秒後に終わる予定（＝３分２０秒の予定）
    - １０操作４０秒後に終わる予定
- 作業速度
    - 開始時
        - **速い**
    - 途中
        - 不安定
    - 終了時
        - ***ヘトヘト***
        - 別の耐久テストもある・・

???

- これを、人力でやってみます
- 都合上、５０回ではなく１０回にします
- **実デバイスデモを実施**
- ***左側のスライドに映す***
- 人間の力を使ってテストを実施する
- １０回くらいモタモタやる
- ストップウォッチでラップを測れたらいいけど、一人じゃ出来ないので頼むか、やらない

---
layout: true
自動テストについて ５０回連続操作
---

## 自動

- １操作６秒
    - ５０操作３００秒（＝５分）
    - １０操作６０秒（＝１分）
- 作業速度
    - 開始時
        - ***比較的遅い***
    - 途中
        - **等速**
    - 終了時
        - 特に問題ない

???

- 次に自動でやってみます
- 都合上、こちらも５０回を１０回にします
- **実デバイスデモを実施**
- ***左側のスライドに映す***
- xcodeでテストを実施
- １０回くらいループ
- ログのタイムスタンプが見せられればいいけど、モタモタからカクカクに変わってる雰囲気が出ればいい

---
layout: true
自動テストについて
---

# 効果的なテスト種類

- 確認
  - 正常系、異常系
  - インテグレーションテスト
- **反復**
  - 正常系、異常系
- **耐久**
  - OutOfMemory
  - 整合性

???

- このように、
- 自動なら１０回操作を
- タイトルで書いていた５０回に増やせますし、
- 果ては１０００回もそれ以上も実行可能です

---
class: middle, center, inverse
layout: true
---
# テストケースについて


???

- では、テストケースの作り方についてお話します

---

layout: true
テストケースについて
---

# ターゲット追加

- `File -> New -> Target -> Test [ iOS UI Testing Bundle ]`

![:style width:70%](new_target.png)

???

- XCodeでUI Testのターゲットを追加してください

---

# マーカー追加

```swift
import UIKit

class ViewController: UIViewController
{
  @IBOutlet weak var addButton: UIBarButtonItem!
  @IBOutlet weak var tableView: UITableView!

  override func viewDidLoad()
  {
    super.viewDidLoad()
    // Do any additional setup after loading the view, typically from a nib.

*    self.addButton.accessibilityIdentifier = "add_button"
*    self.tableView.accessibilityIdentifier = "table_view"
  }
}
```

???

- ソースには、テストケースが参照しやすいようにマーカーを設定します

---

accessibilityIdentifierを実装するクラスたち

![:style ](UIKit.png)

???

- このマーカー
- アクセシビリティ・identifierは、
- どのクラスにもあると言うわけでなく
- UIViewを継承したクラスにだけあります
- 図中には書いていませんが、
- 同様に継承関係にあるクラスを探せば見つかると思います

---

# テストケース作成

```swift
import XCTest
@testable import TaskList

class TaskListUITests: XCTestCase　{
  let app = XCUIApplication()
  // setUp(){..}
  // tearDown(){..}
  func test_foobar()　{
*    let tableView = app.tables["table_view"]
*    let addButton = app.buttons["add_button"]
    // 1. tableView.cellsの現在値を取得する
    let initial_cell_size = tableView.cells.count
    addButton.tap()
    // 1. popupを掴む
    // 2. タイトルを入れる
    // 3. OKをタップ

    // ASSERT: tableView.cellsが１つ増えること
    XCTAssertEqual(tableView.cells.count, initial_cell_size + 1)
  }
}
```

???

- 先ほど設定したマーカーをこのように使って、
- 自動操作するオブジェクトを決めます。
- ボタンをタップするメソッドなどが見えると思います
- ソースには書いていませんが、
- タップの他に、スワイプや、テキスト入力などがあります
- テキスト入力は先程のデモで使っています

---

XCTestのクラス構成

![:style height:150%](XCTest.png)

???

- どのクラスを見れば、
- マーカーでオブジェクトを絞れるかというと
    - この図の通り、私が把握してる範囲では、
    - 大体のクラスで同様に絞れる認識です
- 操作再現系のメソッドを調べるには、
    - XCUIElementを見たらよいでしょう

---

# テストケース生成

- accessibilityIdentifierをUI部品に設定
  ```swift
  alertController.addTextFieldWithConfigurationHandler(
      { (text: UITextField!) -> Void in
        text.accessibilityIdentifier = "alert_textfield"
    })
  ```
- 実行したいTargetを設定
  - ![:style height:20%](target.png)
- TestCaseを開いておく
  - ![:style height:40%](select_ui_testcase.png)
- Record UI Test を実行し、実機を操作する
  - ![:style height:40%](record.png)

???

- XCTestのクラスの扱いが分からなくなった時、
- 参考程度のテストケースをXcodeから生成できます

---

# 生成されたテストケース

```swift
  let app = XCUIApplication()
* app.navigationBars["TaskList.View"].buttons["add_button"].tap()

  let key = app.keyboards.keys["あ"]
  key.tap()
  key.tap()

* let collectionViewsQuery = app.alerts["TODO追加"].collectionViews
* collectionViewsQuery.textFields["alert_textfield"]
  collectionViewsQuery.buttons["OK"].tap()
```

???

- ボタン操作に関してコードに生成してくれるだけで
- テキストフィールドに具体的な文字列を入れるようなコードは生成されませんでした
- よって、
- 参考にするのは、ハイライトの部分で
    - 触ったオブジェクトの
    - identifierの指定方法など
- ここに、代入や検証を追加して
- やっとテストケースになります

---
layout: false

# 自動テストのまとめ

- メリット
  - 苦行の肩代わり
  - 耐久テスト
- デメリット
  - 不安に対する思考停止

???

- 自動テストのメリットは
  - 人力で行おうとすると非現実なことも実施可能であること
- デメリットは
  - 人力ではないので、疲労を感じないこと
  - そこから
  - テスト観点が無くても実施してしまいやすい。


---

class: middle, center, inverse

# ご清聴
# ありがとうございました


