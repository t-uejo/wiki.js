---
title: 【Spring道場】モジュール2：API にセッションベース認証を実装する
description: 
published: true
date: 2024-11-12T13:05:50.147Z
tags: spring boot, spring dojo, spring security
editor: markdown
dateCreated: 2024-10-16T13:09:56.584Z
---

## 実装アウトライン
- ログインのエンドポイントはCSRF対策の対象から除外する（仮実装だったがなぜ必要だった？）
- セッションの保存先を設定する
- セッション固定化攻撃の対策として、ログイン成功後に、新しくセッションを開始する
- `二重送信Cookie（Double Submit Cookie）`を使ったCSRF対策を実装する
- /のエンドポイントへリクエストを投げるとCSRFトークンを返すよう設定
- `AuthenticationManager`経由で認証情報を取得する

## 理解していない点
### セッションベース認証
- ref. [セッションに関する疑問点](/spring-dojo-2-session)

### Spring Boot
- tomcatが内包されている？
- Spring BootにおけるDIの仕組みを実現するCinfigurationクラスの役割とは？
- @Beanや@Componentは何が違うのか？
- Beanがインジェクションされるための条件とは？

### 02-13_セッション固定化攻撃対策をする
- セッション固定化攻撃の対策として、新しくセッションを開始するとあるが、なぜ必要か？
- 新しくセッションを開始するとはどういうことか？
- `setSessionAuthenticationStrategy`メソッドで使う、`SessionAuthenticationStrategy`クラスの初期化する方法として、`ChangeSessionIdAuthenticationStrategy`クラスを見つけたが、これがなぜ`SessionAuthenticationStrategy`クラスの実現クラスと言えるのか？
- ref. [spring-dojo-2-session-fixation-attack](/spring-dojo-2-session-fixation-attack)

### 02-15_CSRF 対策をする
- CSRF対策における同一オリジンポリシーとCORSの関係とは？
	- ref. [spring-csrf](/spring-csrf)

### 02-16_AuthenticationManager 経由で認証情報を取得する
- なぜ`AuthenticationManager`を使う必要があるのか？

### 02-17_ObjectMapper は DI 経由で取得する
- ObjectMapperの挙動が分からないのでJava Docを読んでみる。
- ObjectMapper用のconfigクラスを作ったが、このConfigクラスの役割とどのような単位で作っているのか？

### 02-18_UserDetailsService インターフェースを実装する
- 「ドメインロジックというよりはセキュリティ関連の要請で作られたから`@Service`ではなく、`@Component`をつけた」とはどういうことか？

### 02-20_ユーザー情報をデータベースから取得する
- なぜOptionalでRecordクラスをMapperの戻り値として定義しているのか？
- `Optional<Record>`だと何が嬉しいのか？
- 前回案件でやったときのEntityクラスはRecordクラスとどう違うのか？
- フィールドにfinalをつける理由とは？
- `RequiredArgsConstructor`はfinalかつ初期化されていないフィールドを初期化するためのコンストラクタを生成する？
- Optinalのハンドリング方法について参考になる。
- usernameがNULLだった場合ハンドルしなくていいのだろうか？
	- usernameは主キーのため、NULL条件で検索したときに値が返らないから問題なし。他のクエリなら考慮した方がいいだろう。

### 02-21_認証が必要な API を実装する
- なぜdeniyしたときにforbiddenが返るようにしたのか？

### 02-22_パスワードを安全に保管するための知識
- `BCrypt`やストレッチングとは？
- 3点セットがそれぞれなぜ必要なのか？

### 02-23_ユーザー登録を実装する
- ドメイン層はドメイン的な言葉を使うとあるが、例えば？
- @Transactionalがないとどうなるのか？どういう実装になっているのか？
- なぜResonseEntityでcreatedのときにURIをセットしているのか？

### 02-24_ログアウトを実装する
- どうログアウトを実現しているのかが分からない。セッションに紐づくcookieの削除？
	- ref. [spring-dojo-2-logout](/spring-dojo-2-logout)

  





