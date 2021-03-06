# CDI / Weld

Date: 2015-08-02 23:21
Tags: []
Categories: []

---

## Notes

- @Default
    annotation が記載されていない全Beanに暗黙的に設定される

- @Any について
    > @Anyのありなしについて
    >     @Inject @Any Instance<MyInterface> instanceWithAny;
    >     @Inject      Instance<MyInterface> instanceWithOutAny;
    > @Any は、カスタム限定子を設定したクラスも抽出対象にするかどうかを制御するためのもの。
    > @Any が付いている場合は、カスタム限定子が付与されているクラスも抽出対象になる。
    > 一方、 @Any が付いていない場合は、カスタム限定子を付与したクラスは抽出対象外になり、無理に取得しようとすると例外がスローされる。
- CDI Runner使うときテストクラス自体のScopeが重要(よくそこではまる)

- メンバーにfinal String member = "test";みたいなことをすると想定と違う動きをするので注意(設定されてないことがある？ @PostConstructorで設定しないとダメ？)

Refs:.

- [Weld 2.2.15.Final - CDI Reference Implementation](http://docs.jboss.org/weld/reference/latest-2.2/en-US/html/)
- [JavaEE カテゴリーの記事一覧 - エンタープライズギークス (Enterprise Geeks)](http://enterprisegeeks.hatenablog.com/archive/category/JavaEE)
- [CDI Essential Recipes at Java Day Tokyo 2015](http://www.slideshare.net/OracleMiddleJP/cdi-essential-receipe-at-java-day-tokyo-2015/82)

### 限定子

- 標準の限定子
    - @New
    > @NewアノーテーションはCDIの標準APIとして用意されている限定子で、カスタム限定子を作成する代わりにインジェクション対象のクラス名を直接指定することでインジェクション候補を限定する方法です。この場合、@Newアノーテーションのメンバにクラス名を指定してインジェクションポイントに付与します。
    \* なんか必ず新しいインスタンスが作られちゃうっぽい
    - @Name (非推奨)
    > CDIにはもう一つ@Namedという標準の限定子が用意されており、オブジェクトに名前を付け、その名前で依存関係を解決する方法も用意されています。
    タイプセーフでないから非推奨！

- カスタム限定子 - @Qualifier
    インジェクションする対象を限定する

Refs:. [Java EE 6: Understanding Contexts and Dependency Injection (CDI), Part 2 (Nishigaya's Weblog)](https://blogs.oracle.com/nishigaya/entry/javaee6_understanding_cdi_part_2)

## Errors

### Often

- WELD-001408 Unsatisfied dependencies for type ...
    - 原因) @Injectがあるが、インジェクションしたいクラスが見つからない。Producesメソッドがない、Beanが登録されていない。
- WELD-001409 Ambiguous dependencies for type ...
    - 原因) インジェクション対象が一意に特定できない場合。Producesメソッド、Beanが複数ある。(かつ@Namedなどで特定をしていない)

### Sometimes

- WELD-001410: The injection point [BackedAnnotatedField] @Inject public ... has non-proxyable dependencies
    - 原因) 詳細不明。デフォルトコンストラクタがないとでる。
    - 対策) インタフェースでインジェクトすればでない。

- WELD-000075: Normal scoped managed bean implementation class has a public field:  [EnhancedAnnotatedFieldImpl] ...
    - 原因) 詳細不明。ApplicationScopedでpublic fieldを保持するとでるっぽい。(JUnitのCDI Runnerでテストクラス自体をApplicationScopedにすると@Ruleが使えなくなる。。)

## Refs

- [CDI を理解する為に重要なレシピ](http://yoshio3.com/2015/04/15/cdi-essential-recipes/)

