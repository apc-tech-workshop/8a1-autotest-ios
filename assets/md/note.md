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
- 元プロジェクトでObjective-C, Swiftで自動UIテストを実施していた
- 難しいのかな？と思っていたが意外と簡単だった
- 書き方が分からなくてもヒントはXcodeがくれる事が分かった
- **序盤だけでも共有したい**

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

- では、テスト自体についてサラッとご説明致します

---

layout: true
テストについて
---

# カテゴリ

- 単体テスト

???
- テストには、
- ロジック確認の単体テスト
- 部分シナリオでのUIテスト
- end to endのシナリオでのインテグレーションテスト
- があります。

--
- UIテスト

--
- インテグレーションテスト

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

???

- そして、
- テストの種類には
- 実装の確認
- 冪等性やデグレ確認の反復
- 耐久性確認
- があります。

--
- 反復
  - 正常系、異常系

--
- 耐久
  - OutOfMemory
  - 整合性

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
---

layout: true
自動テストについて
---

# ５０回連続操作して<br>OutOfMemory</span><br>の発生可否を確認する


- 負荷を掛けてメモリ解放の問題を探す
- インフラレベルでのボトルネックを探す
- ~~思いつき・水増し・不安解消~~

???

例えば、耐久テストに同じ操作を繰り返して、メモリ解放が適切か確認するものが有ります。

---
layout: true
自動テストについて ５０回連続操作
---

## 他人力＆自力

- １操作４秒で、５０操作２００秒後に終わる予定（＝３分２０秒の予定）
- 作業速度
    - 開始時
        - **速い**
    - 途中
        - 不安定
    - 終了時
        - ***ヘトヘト***
        - 別の耐久テストもある・・

---
layout: true
自動テストについて ５０回連続操作
---

## 自動化

- １操作６秒で、５０操作３００秒（＝５分）
- 作業速度
    - 開始時
        - ***比較的遅い***
    - 途中
        - **等速**
    - 終了時
        - 特に問題ない

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

---
class: middle, center, inverse
layout: true
---
# テストケースについて
---

layout: true
テストケースについて
---

# ターゲット追加

- `File -> New -> Target -> Test [ iOS UI Testing Bundle ]`

![:style width:70%](new_target.png)

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

---

accessibilityIdentifierを実装するクラスたち

![:style ](UIKit.png)

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

---

XCTestのクラス構成

![:style height:150%](XCTest.png)

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

---

# 生成されたテストケース

- 参考にするのは、ハイライトの部分
- オブジェクトの構造、ID指定取得など

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
- どのオブジェクトに何を入力するかは記録されなかった
- このまま利用しても有効なコードにならない


---
layout: false

# まとめ

- 自動テストのメリット
  - 苦行の肩代わり
  - 耐久テスト
- 自動テストのデメリット
  - 不安に対する思考停止

???

- メリットは
  - 一見無駄っぽい苦行系テストを人間にさせなくて済むこと
  - テスターが耐えられない耐久テストも行えること
- デメリットは
  - 自動なので、テスト観点が無くても実施してしまいやすい。
