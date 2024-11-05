---
title: 【Spring道場】モジュール3：Integration Test を実装する
description: 
published: true
date: 2024-11-05T13:16:55.788Z
tags: spring dojo
editor: markdown
dateCreated: 2024-11-01T04:21:07.502Z
---

- なぜカバレッジを追求するのは良くないのか？

## 03-10_Spring での統合テスト
- Filter→Controllerのテストは統合テストと言うのか？
- Filterだけのテストは意味がないのか？

## 03-11_@SpringBootTest を付与したテストクラスを作成する
- `ApplicationContext`とは何か？
- `@SpringBootApplication`とは何か？どのような関係があるか？
- なぜ`@SpringBootTest`を使用して、ApplicationContextを作りたいのか？
- テストコードではAutowiredを使う理由は何か？そもそもなぜプロダクションコードでは、@Autowiredではなく、@RequiredArgsConstructorを使うのか？
- 