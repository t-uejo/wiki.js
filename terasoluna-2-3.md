---
title: 【TERASOLUNA】2.3. はじめてのSpring MVCアプリケーション
description: 
published: true
date: 2024-11-20T12:39:33.493Z
tags: terasoluna, spring mvc
editor: markdown
dateCreated: 2024-11-20T11:31:03.707Z
---

## 公式ドキュメント
- https://terasolunaorg.github.io/guideline/current/ja/Overview/FirstApplication.html

## SpringMvcConfigとは？
- Spring MVCの設定を行うためのconfigクラス。
- `todo\src\main\java\com\example\todo\config\web\SpringMvcConfig.java`
- 以下のようにクラス定義となる。
```java
/**
 * Configure SpringMVC.
 */
@ComponentScan(basePackages = { "com.example.helloworld.app" }) // (2)
@EnableAspectJAutoProxy
@EnableWebMvc // (1)
@Configuration
public class SpringMvcConfig implements WebMvcConfigurer {

}
```

## @ComponentScanとは？
- 指定されたパッケージをスキャンし、そこに定義されているSpringコンポーネント（@Component、@Controller、@Service、@Repositoryなどが付与されたクラス）を自動的に検出し、Springのアプリケーションコンテキストに登録するための仕組み。

### @ComponentScanを使うメリットとは？
- 手動で@Beanを登録する場合メソッドごとに設定をしていかなければならない。
- 仮に@ComponentScanを使わない場合、いくつものController、Service、Repositoryクラスを管理するConfigクラスを用意して、1つずつ登録していかなければならない。
- そのような煩雑さをなくすのが@ComponentScanである。
- クラスに@Controllerなどを付与するだけで自動で検出され、Springコンテナに登録することができる。
- 手動管理から解放される。

## ViewResolverとは？
- ViewResolverがビュー名を解析し、対象のビューを決定する。

## Thymeleafにおける各フィールドについて
```java
<!DOCTYPE html>
<html xmlns:th="http://www.thymeleaf.org"> <!--/* (1) */-->
<head>
<title>Echo Application</title>
</head>
<body>
    <!--/* (2) */-->
    <form th:object="${echoForm}" th:action="@{/echo/hello}" method="post">
        <label for="name">Input Your Name:</label>
        <input th:field="*{name}"> <!--/* (3) */-->
        <input type="submit">
    </form>
</body>
</html>
```
### (2)について
- 以下の(2)では、th:object属性にフォームオブジェクトの名前を指定している。

### (3)について
- > ユーザーが入力した値は、フォームの送信時に name フィールドとしてサーバーに送信され、echoForm オブジェクトの name プロパティに自動的にマッピングされます。
- > name プロパティにバインドする役割を持ち、データの双方向のやり取り（表示と送信）を容易にする。
- また、短縮記法を使っているらしく、
- > *{name} は、フォーム全体に設定された th:object="${echoForm}" のオブジェクトから、name プロパティを参照しています。この短縮記法により、th:object を基準にプロパティを記述できるようになります。











