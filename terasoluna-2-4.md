---
title: 2.4. アプリケーションのレイヤ化
description: 
published: true
date: 2024-11-26T11:07:49.923Z
tags: 
editor: markdown
dateCreated: 2024-11-26T10:57:34.913Z
---

## 設計思想
- ドメイン層が他の層に依存してはいけない。
- アプリケーション層で行う実装はできるだけ薄く保つ。ビジネスルールを含んではならない。以下のような機能が中心。
  - データの入出力を行う UI(User Interface)の提供
  - クライアントからのリクエストハンドリング
  - 入力データの妥当性チェック
  - リクエスト内容に対応するドメイン層のコンポーネントの呼び出し
- Form オブジェクトは、リクエストパラメータを保持する POJO クラスが該当。form backing bean と呼ばれる。

## 変換処理と Helper

- アプリケーション層がドメイン層に依存しないためには、以下のような変換処理を実施する。
  - Form から Domain Object(Entity 等)への変換処理
  - Domain Object から Form への変換処理
- しかし、変換処理が長くなると Controller 処理の見通しが悪くなる。
- その場合に、Helper や MapStcuct を活用する。
- Helper は Controller の見通しを良くするためのものであるため、Helper は Controller の一部として扱ってよい。

## Bean マッピング(MapStruct)

- ドメイン層は、アプリケーション層に依存してはならないため、Form オブジェクトをそのままドメイン層で使用してはならない。
- アプリケーションの異なるレイヤ間(アプリケーション層とドメイン層)で、データの受け渡しをする場合など、Bean マッピングが必要となるケースは多い。
- Setter や Getter を利用した Bean マッピングを行うと実装が煩雑になる。
- プログラムの見通しが悪くなるため、本ガイドラインでは OSS で利用可能な Bean マッピングライブラリとして MapStruct を使用することを推奨している。

### コード例

MapStruct を使用した場合と使用しない場合のコード例。

- 煩雑になり、プログラムの見通しが悪くなる例

```java
Source source = userService.findById(userId);

Target target = new Target();

target.setId(source.getId());
target.setPerson(new Person(source.getPersonForm().getCode(), source.getPersonForm().getName()));
target.setOrders(new HashSet<>(source.getOrders()));
```

- MapStruct を使用した場合の例

```java
@Mapper
public interface BeanMapper {

    Target map(Source source);

}
```

```java
Source source = userService.findById(userId);
Target target = beanMapper.map(source);
```

### Lombok が機能しない事象

- > maven-compiler-plugin では、mapstruct プロセッサのみを使用し Lombok プロセッサを使用しない状態になり、Lombok が動作しなくなる。

### maven-compiler-plugin とは？

- > compile フェーズや test-compile フェーズで実行され、指定されたソースコード（通常は src/main/java ディレクトリ内）をコンパイルして、target/classes ディレクトリにクラスファイルを生成します。

## マッパー生成処理

- > 生成されるクラスは target/generated-sources/annotations 配下のマッパーインタフェースと同じパッケージに配置される。そのため、マッパーインタフェースは component-scan の対象となるパスに配置をする必要がある。

### なぜ、マッパーインターフェースを component-scan の対象となるパスに配置をする必要があるのか？
- MapStruct が生成したマッパークラスは、Spring の DI コンテナに登録されて、他のクラスから依存注入されるべきであり、インターフェースが属するパッケージと同等の構造に.class が作成されるため。

## 依存注入方法

- なぜ@Ingect なのか。@Autowired とかではだめなのか。
- @RequiredArgsConstructor でも問題なくいけた。

## トランザクション境界

- > 「オブジェクトがトランザクション境界となる」とは、そのオブジェクトがデータ操作の単位であり、そのライフサイクルに合わせてトランザクションを開始、管理、終了することを意味します。

- Spring ではトランザクション管理をサービス層のメソッドで行う。
- ドキュメントではこれを「Service のメソッドをトランザクション境界にする」と言っている。

## Mybatis はなぜ ORM ではないか？

- 厳密には ORM でないという。
- SQL 文自体は存在し、結果の Mapping を行っているから。
- .NET の Entityfrawework は SQL 文を扱わないから、完全な ORM であるといえる。

## 呼び出し可否ルール

- > 注意するべきことは、基本的に Service から Service の呼び出しは、禁止している点である。
- > ルールを守らない場合、開発規模が大きくなった際に、修正の影響範囲が分かりにくくなったり、横断的な共通処理を追加しにくくなるなど、
- > 保守性に大きな問題が生じることが多い。後で問題にならないように、初めから依存関係に気を付けて開発することを強く推奨する。

## プロジェクト構成

- > 通常 infra プロジェクトを隠蔽化する必要がなく、domain プロジェクトに格納されている方が開発しやすい。
- 参照順序をつけるとは？