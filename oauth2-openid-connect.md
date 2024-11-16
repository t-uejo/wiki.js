---
title: 【Udemy】手を動かして理解する！OAuth2 / OpenID Connect の基礎と活用
description: 
published: true
date: 2024-11-16T02:50:44.101Z
tags: oauth2, open id connect
editor: markdown
dateCreated: 2024-11-04T03:26:29.847Z
---

## OAuth2の仕組み
### なぜ認可コードが必要なのか？
- アクセストークンをブラウザに渡すと盗まれるなどの危険性があるため、ブラウザに触れさせずにしたいから。
- 認可コードをブラウザ側で扱うが、それが盗まれたら、アクセストークンを取得されてしまうのでは？この懸念はあるのか？
