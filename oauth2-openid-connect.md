---
title: 【Udemy】手を動かして理解する！OAuth2 / OpenID Connect の基礎と活用
description: 
published: true
date: 2024-11-17T01:20:00.307Z
tags: oauth2, open id connect
editor: markdown
dateCreated: 2024-11-04T03:26:29.847Z
---

## OAuth2の仕組み
### なぜ認可コードが必要なのか？
- アクセストークンをブラウザに渡すと盗まれるなどの危険性があるため、ブラウザに触れさせずにしたいから。

#### どんなリスク？
- HTTPSを使えばリスクは減らせるが、HTTPなどを使うと盗まれるリスクあり。
- XSSなどの攻撃で抜き取られるリスクあり。

### 認可コードはブラウザ側で扱うが、それが盗まれたら、アクセストークンを取得されてしまうのでは？
- それがないように様々な仕組みが施されている。
- 例えば、
	- 発行されてから短時間で無効にする
  - 有効期限は最大でも10分を推奨
  - 
  
 ### ref
 https://openid-foundation-japan.github.io/rfc6749.ja.html