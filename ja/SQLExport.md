---
title: 外部SQLデータベースへの書き出し
---

# 外部SQLデータベースへの書き出し

JabRefは、BibTeXデータベースの内容を、グループ情報とともに、外部のMySQLやPostgreSQLデータベースに書き出すことができます。

ただし、MySQL若しくはPostgreSQLサーバーの全権限を持つユーザー名とパスワードを持っていることが必要です。

## 書き出し

1.  **ファイル→外部SQLデータベースに書き出す**を選択するか、ツールバーの対応するボタンを押してください。
2.  **サーバー型**ドロップダウンメニューからデータベースの型を選択してください。
3.  データベース接続情報を入力し、**接続**を押してください。

すると、JabRefは指定されたデータベースに接続し、新規テーブルを作成し、それらのテーブルに項目とグループ情報を格納します。それ以前に書き出したデータを失うことなく、好きなだけ多くのJabRef書誌情報データベースを書き出すことができます。システムは、フルパス(ディレクトリ構造+ファイル名)を使ってデータベースを一意に識別します。同じJabRefデータベースを二度以上書き出すと、SQLデータベース内のそのデータベースのデータが更新されます。なお、続けて書き出す場合には、接続情報を入力するようには促されません。別のデータベースに書き出したい場合には、**ファイル→外部SQLデータベースに接続**を選択して(若しくは対応するツールバーボタンを押して)、書き出しを実行してください。第2.8版以降では、テーブルはドロップされませんので、二つ以上のJabRefデータベースを同一のSQLデータベースに保管することができます。

SQLデータベースからデータベースを読み込む場合(**ファイル→外部SQLデータベースから読み込む**)には、読み込まれた各データベースを別々のタブに収録します。