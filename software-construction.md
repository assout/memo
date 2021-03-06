# Software construction

Date: 2014-12-18 15:45
Tags: []
Categories: []

---

## Prelude

- Software testingについては [software-testing](software-testing)

## Process - ソフトウェア開発プロセス

### SLCP-JCF - 共通フレーム

「保守・運用」とまとめることが多いが、共通フレームではそれを明確に区分している。
「保守」とはシステムを改善・変更する作業
「運用」は現行のシステムを日々動かしていく作業。システムの変更作業はしない

Refs: [共通フレーム＜法規・基準＜Ｗｅｂ教材＜木暮仁](http://kogures.com/hitoshi/webtext/std-kyotu-frame/index.html)

## Requirement definition - 要件定義

要求仕様書は取得者が供給者に対して求めるシステムの機能を記述したものであり、要件定義書は、開発されるべきシステムの機能を定義したものである。

- 要求定義 : 「～がしたい」 -> 利用者の希望
- 要件定義 : 「～が必要」 -> システムの仕様書

RFI / RFP

- RFI - Request For Information - 情報提供依頼書 : 顧客が作成
- RFP - Request For Proposal - 提案依頼書 : ベンダーが作成

## Design - 設計

### Naming - 名前付け

#### 追加

- set        : 主にクラスのプロパティに値を代入する場合に用いる。
- add        : 追加。配列・リストにオブジェクトを加えるケースが多い。数値の加算もこちらを用いる。
- insert     : 配列・リストなどの任意の位置に挿入する。データベースへの新規追加を指す場合もある。
- append     : 末尾に追加する。
- prepend    : 先頭に追加する。
- create     : パラメータを元にデータを作成して返す。追加処理まで行うケースも有る。
- register   : 登録。データベースにユーザー等の情報を登録するなど。

#### 保存・出力

- save       : 状態の保存。ファイル全体を保存する場合など。
- export     : 書き出し。形式を変換したり任意の形式で保存する。
- output     : 出力。スクリーンへの出力・ファイルへの出力を指すことが多いが用途の広い単語。
- write      : 書き込み。一行単位で追加書込することを示すことが多い。

#### 読み込み・解析

- get        : クラスプロパティなどを読み取る。
- load       : ファイル全体を読み込む場合など。
- import     : ファイルを対応形式に変換して読み込む。
- read       : ファイルから一行取り出す。
- parse      : 分解して解析する。XML を要素ごとに分ける場合など、何らかの区切りをもとに分析する。

#### 編集・変更・修正

- update     : 情報の更新。データベースの既存レコードを変更する場合など。
- edit       : データの書き換え。データベースのカラム単位で書き換える場合など。
- change     : 全く別の状態に変える。新しいデータで置き換えて古いデータは消滅する。
- modify     : 部分的に修正する。edit より範囲が狭い。１項目の変更など。
- replace    : 順序・文字の入れ替え。
- join       : データを前方又は後方に付け足す。
- merge      : 複数のデータを結合する。データはソートにより混ざり合って継ぎ目がわからなくなる。
- normalize  : 値を定められた範囲内に収める。
- increase   : 数量を増加させる。継続的に増加し続けるというニュアンスも持つ。
- reduce     : 数量を減少させる。increase の反意語には decrease もあるが、そちらは徐々に減少するというニュアンスを持つ。
- adjust     : 値を調整する。何らかの目的に合うまで値を増減させる。
- fix        : 破損したデータを修復する。
- correct    : 誤りのあるデータを正しく直す。
- convert    : 別の形式に変換する。
- enable     : 機能を有効にする。使用可能にする。
- disable    : 機能を無効にする。使用を停止する。
- apply      : 適用する。当てはめる。

#### 削除

- delete     : 完全な削除。元に戻すことはできない。
- remove     : データをリストや閲覧・アクセス可能な場所から取り除く。アクセス権のない領域への移動。取り除かれたデータが消滅するとは限らず、元に戻せる可能性がある。「帽子を脱ぐ」「靴を脱ぐ」も remove だが帽子や靴は消えない。
- clear      : 中身を空にする。親となるオブジェクトや変数自体は消えない。
- unregister : 登録を解除する。
- unset      : セット済みのプロパティ、定義済みの変数をセット前、未定義の状態に戻す。あるいは参照を解除する。

#### 検索

- find       : 情報の中から探し出す。見つかることが前提。
- search     : 情報の中に存在するか探してみる。無いかもしれない。
- extract    : 条件による抽出。対象となる連想配列、オブジェクトから特定のキー、フィールドの値を取り出す。
- filter     : 条件による除外。条件に合わないものを隠す。
- seek       : 連続したデータの中からあるデータが見つかるまで順番に探査する。

#### 検査

- is～       : オブジェクトが特定の型、状態であるか調べて true/false を返す。
- has～      : オブジェクトが特定のプロパティを持っているかを調べて true/false を返す。権限、属性の所有を確認する。
- contains   : 配列に特定の値が含まれているかを調べて true/false を返す。
- ～exists   : 項目の有無を調べる。
- check      : 広い意味での確認。validate が対象の正しさを検証するのに対し、check は対象が真か偽を調べたり、単に変数に何が入っているかを知るために使われる。
- validate   : 正しいものであるか確かめる。決められたフォーマットや正しくルールに従っているか、要件や性能を満たしているかを調べる、妥当なら valid、過不足があれば invalid（true/false）
- verify     : 正しく動作しているか確かめる。入力に対し正しい出力が行われているか検証し、正しければ correct、問題があれば incorrect（true/false）

#### その他

- exec       : 処理、命令、外部アプリケーションの実行。=execute。
- run        : スクリプト、コマンドの実行（インタプリタであることが多い）
- init       : 初期化する。デフォルトとなる値をセットする。=initialize。
- reset      : 既に初期化されたものに初期値をセットし直す。
- build      : クエリ、構文を組み立てる。ソースコードをバイナリ化することを指す場合もある。
- open       : ソケットなどの通信、ストリームへの接続。
- close      : ソケットなどの通信、ストリームの終了・切断。

#### Refs:

- [関数名によく使われる英単語（動詞）の意味とニュアンス](http://php-archive.net/php/words-in-function-names/)
- [正しいコーディングが身につくエンジニア英語の手引き 〜文法とクラス／メソッド、命名規則〜](http://www.find-job.net/startup/ehce]nglish-for-engineers-naming-conventions)
- [メソッドに名前を付けるときは英語の品詞に気をつけよう](http://qiita.com/jnchito/items/459d58ba652bf4763820)
- [モデルやメソッドに名前を付けるときは英語の品詞に気をつけよう](http://qiita.com/jnchito/items/459d58ba652bf4763820?utm_content=buffer31738&utm_medium=social&utm_source=twitter.com&utm_campaign=buffer)

### 凝集度、結合度

#### 凝集度

- 偶発的凝集（Coincidental Cohesion）「最悪」
    > 適当（無作為）に集められたものがモジュールとなっている。モジュール内の各部分には特に関連性はない（例えば、よく使われる関数を集めたモジュールなど）。
- 論理的凝集（Logical Cohesion）
    > 論理的に似たようなことをするものを集めたモジュール（例えば、全ての入出力ルーチンを集めたモジュールなど）。
- 時間的凝集（Temporal Cohesion）
    > 動作させたときにモジュール内の各部分が時間的に近く動作する（例えば、ある例外を受けたときに動作するルーチンとして、ファイルをクローズするルーチン、エラーログを作成するルーチン、ユーザーに通知するルーチンなどを集めたモジュール）。
- 手続き的凝集（Procedural Cohesion）
    > ある種の処理を行うときに動作する部分を集めたモジュール（例えば、ファイルのパーミッションをチェックするルーチンとファイルをオープンするルーチンなど）。
- 通信的凝集（Communicational Cohesion）
    > 同じデータを扱う部分を集めたモジュール（例えば、同種のレコードの情報を操作するルーチンを集めたモジュールなど）。
- 逐次的凝集（Sequential Cohesion）
    > ある部分の出力が別の部分の入力となるような部分を集めたモジュール（例えば、全体としてあるファイルを読み込んで処理をするモジュール）。
- 機能的凝集（Functional Cohesion）「最善」
    > 単一のうまく定義されたタスクを実現するモジュール（例えば、角度のサインを計算するモジュール）

>凝集度は必ずしも上記の順に高いとか低いと言えるものではない。Larry Constantine やエドワード・ヨードンや他の人々の研究によると、上記の最初の2つは他の凝集よりも劣っており、通信的凝集以下の3つはそれ以外よりも優れている。いずれにしても7番目の機能的凝集が最も優れているとされる。

#### 結合度

##### 手続き型プログラミング

- 内容結合（Content coupling）「高」
    > 病理学的結合とも呼ばれ、あるモジュールが別のモジュールの内部動作によって変化したり依存したりする(例えば別のモジュールの内部データを直接参照する)。したがって、第2のモジュールは、データを生成する方法（場所、種類、タイミング）を変更すると、依存モジュールを変更することにつながる。
- 共通結合（Common coupling）
    > グローバル結合とも呼ばれ、二つのモジュールが同じグローバルデータ（例えば、グローバル変数）を共有する。共通のリソースを変更すると、それを使用したすべてのモジュールを変更することを意味する。
- 外部結合（External coupling）
    > 二つのモジュールは、外部から供給されたデータ·フォーマット、通信プロトコル、またはデバイスインターフェイスを共有している場合に起こる。 これは基本的に外部ツールやデバイスへの通信に関連している。
- 制御結合（Control coupling）
    > あるモジュールに何をすべきかについての情報（例えば、処理を制御するためのフラグ）渡すことで、別のモジュール処理の流れを制御する。
- スタンプ結合（Stamp coupling）
    > 複数のモジュールが複合データ構造を共有し、その一部のみを使用する(例えば、全レコードの中の1つのフィールドを必要とする関数に全レコードのデータの構造体を渡す)。異なる部分も使用可能。これは、モジュールが必要としないフィールドが変更されることにより、モジュールのレコードを読み取る方法を変更することにつながる可能性がある。
- データ結合（Data coupling）
    > モジュールを介してデータを共有する場合、例えば、引数である。 各データは基本部分であり、これらは単純なデータの受け渡しのみを行う（例えば、数値を渡してその平方根を返す）。
- メッセージ結合（Message coupling）「低」
    > 最も結合度が低い結合の種類である。（引数のない）メソッドの呼び出し。メッセージパッシング。
- 無結合（No coupling）
    > モジュールが相互に全く通信を行わない。

##### オブジェクト指向プログラミング

- サブクラス結合（Subclass Coupling）
    > 子クラスとその親クラスとの間の関係で、子クラスは、その親クラスに依存しているが、親クラスが子クラスを知らない状態。子クラスが親クラスに依存しすぎると、親クラスを修正するのが難しくなる。
- 一時的結合（Temporal coupling）
    > あるメソッドが別のメソッドに依存すること（例えば、executeしないとerrorが取得できない）。

### Design Pattern

Refs: [Text 2 Mind Map - Design Pattern](http://www.text2mindmap.com/w2dArcX)

```
Design Pattern
    GOF
        生成に関するパターン
            Abstract Factory - 関連する一連のインスタンスを状況に応じて適切に生成する方法を提供する
            Builder
            Factory Method
        構造に関するパターン
            ...
        振る舞いに関するパターン
            ...
    マルチスレッドプログラミングに関するパターン
        ...
```

### Exception - 例外設計

Refs:

- [Ruby - Railsアプリケーションにおけるエラー処理（例外設計）の考え方 - Qiita](http://qiita.com/jnchito/items/3ef95ea144ed15df3637)
- [.NETの例外処理 Part.1 - とあるコンサルタントのつぶやき - Site Home - MSDN Blogs](http://blogs.msdn.com/b/nakama/archive/2008/12/29/net-part-1.aspx)

## Implementation - 実装

### Commit comment

- [Gitのコミットメッセージの書き方 - Qiita](http://qiita.com/itosho/items/9565c6ad2ffc24c09364)
- [Subversion - コミットメッセージの作法 - Qiita](http://qiita.com/suin/items/b3619ddaa176fef519cb)
- [awesome-commit-english/README.md at master · azu/awesome-commit-english · GitHub](https://github.com/azu/awesome-commit-english/blob/master/README.md)
- [vcs - オレオレコミットメッセージの生煮え書き方 - Qiita](http://qiita.com/yshr04hrk/items/39e54334b98f43544f22)

#### Format

1行目 : 変更内容の要約（タイトル、概要）。
2行目 : 空行
3行目以降 : 変更した理由（内容、詳細）

#### Words

簡易版

- add            : 新規（ファイル）機能追加
- fix            : バグ修正
- major changes  : 大きな変更
- minor changes  : 小さな変更
- modify(change) : 機能修正（バグではない）
- remove         : 削除（ファイル）

詳細版

- add     : 新規（ファイル）機能追加
- change  : 仕様変更
- clean   : 整理（リファクタリング等）
- disable : 無効化（コメントアウト等）
- fix     : バグ修正
- hotfix  : クリティカルなバグ修正
- modify  : 機能修正（バグではない）
- remove  : 削除（ファイル）
- revert  : 変更取り消し
- upgrade : バージョンアップ

使っちゃいけない単語

- change/modify : ざっくりすぎて意味無い

#### 7 rules

1. subjectとbodyは1行あけましょう
2. subjectは50文字以内にしましょう
3. subjectの1文字目は大文字にしましょう
4. subjectにperiodは不要です
5. subjectは命令形にしましょう
6. bodyは1行あたり72文字以内にしましょう
7. howよりwhatやwhyをbodyに記述しましょう

Refs: [Gitコミットメッセージの7大原則 - rochefort&#39;s blog](http://rochefort.hatenablog.com/entry/2015/09/05/090000)

### Pull Request Template - プルリクエストテンプレート

Refs:

- [Pull Request のフォーマットを決めるとレビューの効率が3倍よくなる :: Crocos Engineering Blog](http://engineering.crocos.jp/post/98455177675/pull-request-%E3%81%AE%E3%83%95%E3%82%A9%E3%83%BC%E3%83%9E%E3%83%83%E3%83%88%E3%82%92%E6%B1%BA%E3%82%81%E3%82%8B%E3%81%A8%E3%83%AC%E3%83%93%E3%83%A5%E3%83%BC%E3%81%AE%E5%8A%B9%E7%8E%87%E3%81%8C3%E5%80%8D%E3%82%88%E3%81%8F%E3%81%AA%E3%82%8B)
- [symfony/CONTRIBUTING.md at 2.8 · symfony/symfony · GitHub](https://github.com/symfony/symfony/blob/2.8/CONTRIBUTING.md)
- [パッチの投稿 Symfony2日本語ドキュメント](http://docs.symfony.gr.jp/symfony2/contributing/code/patches.html)

### READMEの書き方

- プロジェクトの見出し(Project Heading)
- 目次(Table of Contents)
- 必要条件(Requirements)
- 使い方(Usage)
- その他の節
    - なぜ？ (Why?)
    - よくある質問(Common Questions)
    - 例(Examples)

Refs: [読みやすいREADMEを書く | Yakst](https://yakst.com/ja/posts/3859)

## Review - レビュー

| 公式度     | 名称               | 説明                                                                                                                                                                                                                                                                                 |
|------------|--------------------|--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| 最も公式   | インスペクション   | 最も体系的で厳格です。作成者以外の参加者はミーティング時に役割が与えられます。モデレーターがミーティングを主導し、読み手が資料を提示して自分の解釈で説明します。そしてレビュアが指摘した問題点などは、書記が記録します。発見された欠陥はデータとして収集して、分析をおこないます。 |
|            | チームレビュー     | 公式なレビューですが、インスペクションほど厳格ではありません。 作成者がモデレーターを兼ねてかまいませんし、読み手の役割は存在せずモデレーターが資料を説明していきます。記録はしますが、そのデータの収集、分析は必要とされていません。                                                |
|            | ウォークスルー     | 非公式なレビューです。作成者が成果物を同僚に説明してコメントをもとめます。 インスペクションがチームの品質の満足にあるのに対して、ウォークスルーは作成者の満足を求めるものです。 通常、定義された手順も存在せず、記録もしません。                                                     |
|            | ペアプログラミング | ペアプログラミングも一種の非公式なレビューといえます。                                                                                                                                                                                                                               |
|            | ピアデスクチェック | 机上チェック。自分で書いたものを自分で丹念に調べる                                                                                                                                                                                                                                   |
| 最も非公式 | アドホックレビュー | 即席のレビュー。つかまえにくいバグをつきとめるのに同僚にチェックを頼む行為があたります。 プロセスとして組み込まれておらず、目下の問題の解決以上の成果はないです。                                                                                                                    |

Refs: [あなたのおっしゃるレビューってどのことかしら？ - Qiita](http://qiita.com/mima_ita/items/c3490ad1ccc12ad853f1)

## OOP - オブジェクト指向プログラミング

CRCカード(Class Responsibility Collaborator)
> クラス (class) は同じようなオブジェクトの集合であり、責務 (responsibility) はクラスが知っている、あるいは行う事柄であり、協調クラス (collaborator) はクラスが責務を果たすために相互作用する他のクラスです

Refs: [CRC(Class Responsibility Collaborator)モデルの概要](https://www.ogis-ri.co.jp/otc/swec/process/am-res/am/artifacts/crcModel.html)

## Concurrent Programing - 並行プログラミング

並行(concurrent)と並列(parallel)の違い

- 並列(parallel) - 処理能力向上のため「新に同時進行的な処理」
- 並行(concurrent) - 論理的に同時進行的な処理。「疑似並列」
    - e.g. 複数スレッドコンテキストスイッチしながら同時に処理してるように見える など

Refs: [parallel と concurrent、並列と並行の違い - 本当は怖い情報科学](http://freak-da.hatenablog.com/entry/20100915/p1)

## Log

- INFOログから書いてく

    Refs: [良いデバッグログはプロジェクトの資産である // Speaker Deck](https://speakerdeck.com/yhara/liang-idebatuguroguhapuroziekutofalsezi-chan-dearu)

- エラーメッセージは2W1Hで書く。

        what => 'What happened?',
        why  => 'Why did this happen?',
        how  => 'How can we support this?',

    Refs: [エラーメッセージは 2W1H がいいんじゃないか - @bayashi Diary](https://bayashi.net/diary/2016/0719)

## Refs

- [雑把の UI アーキテクチャー史(MVCからMVVMへ) プログラマーズ雑記帳](http://yohshiy.blog.fc2.com/blog-entry-215.html)
- [ライブラリー、ツールキット、フレームワーク 違いわかる? プログラマーズ雑記帳](http://yohshiy.blog.fc2.com/blog-entry-214.html)
- [- 技術文書_タイトル](http://objectclub.jp/technicaldoc/)
