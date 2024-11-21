---
title: Maven 入門：Java初心者から！Spring Bootを用いて開発に必須のビルドツールをintelliJで学ぼう。
description: 
published: true
date: 2024-11-21T13:30:22.348Z
tags: maven
editor: markdown
dateCreated: 2024-11-21T13:01:56.712Z
---

## POMとは？
- Project Object Modelの略。
- Project Object Modelにおける「モデル」とは、物事を理解しやすくするために、その構造やルールを簡略化した表現。
- Mavenでプロジェクトを管理するための設計図であり、その構造を「モデル」と呼んでいる。

## 推移的依存関係とは？
- ライブラリが依存するライブラリのこと。
- 前にDBUnitを使ったことがあったが、その依存先としてロガーのライブラリなど4つほど必要だった。
- そういった依存が複数存在した場合、手動で解決するのは面倒で煩雑な作業である。
- Mavenを使えば自動で解決することができる。