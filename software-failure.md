---
title: ソフトウェア開発現場の「失敗」集めてみた。 42の失敗事例で学ぶチーム開発のうまい進めかた
description: 
published: true
date: 2024-11-14T11:26:02.532Z
tags: 
editor: markdown
dateCreated: 2024-11-14T10:47:21.069Z
---

## 不完全リポジトリ
- ソースコード以外の断片的なツールをリポジトリで管理しておいてよかった。
- 作った人のPCに残ったままで復元できないとか、ファイルサーバにあるが、どこにあるか分からいといった手間が発生するリスクが高いため。
- コードや環境構築などに関わる情報はどんどんリポジトリにおいておく。数年後誰もいなくなっても環境構築ができるように情報を残す。

## 経験値泥棒
- 環境構築、アーキテクチャ設計、プログラム設計など。
- 自分がやった方が早いといった理由でやるのは、短期的にはいいかもしれないが、長期的に組織全体の開発力、設計力が落ちることになる。