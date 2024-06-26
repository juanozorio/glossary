---
title: eBPF
status: Completed
category: テクノロジー
tags: ["アーキテクチャ", "ネットワーキング", "セキュリティ"]
---

eBPF (extended Berkeley Packet Filter)は、Linuxカーネルのソースコードを修正したりカーネルモジュールを導入したりすることなく、サンドボックス化された小さなプログラムやスクリプトをLinuxシステムのカーネル空間で実行できる技術です。

Linuxシステムには2種類の空間があります。カーネル空間とユーザー空間です。
カーネルはOSのコアにあたり、ハードウェアに無制限でアクセスできる唯一の部分です。

アプリケーションはユーザー空間で動作し、高位の権限が必要な場合にカーネルへ要求を送ります。
ハードウェアへの直接アクセスなど、より柔軟性を必要とするアプリケーションについては、「Linuxカーネルモジュール」として知られるアプローチでカーネルを拡張することができます。
このアプローチによりカーネルの標準機能は拡張され、アプリケーションは基礎となる要素へより深くアクセスできるようになります。
しかしこのアプローチはセキュリティリスクももたらすため、eBPFが魅力的な代替となります。

## 解決すべき問題はなんですか

一般的に、アプリケーションはユーザー空間で動作し、アプリケーションがカーネルから(例えばハードウェアへのアクセスなどの)権限を要求するときは、いわゆる「システムコール」を介して要求します。
多くの場合、このアプローチはうまく働きますが、低水準なシステムに対するより柔軟なアクセスを開発者が必要とする場合があります。
オブザーバビリティ、セキュリティやネットワーク機能はこういった場合の良い例です。
この実現のため、Linuxカーネルモジュールを使ってカーネルのソースコードを修正することなくカーネルの基礎を拡張することができます。
Linuxカーネルモジュールの使用には利点もありますが、セキュリティリスクももたらします。
Linuxカーネルモジュールはカーネル空間の内部で動作するため、カーネルをクラッシュさせる可能性があり、カーネルがクラッシュするということは機器全体もクラッシュすることになります。
加えて、カーネルモジュールは特権を持ち、システムリソースに直接アクセスします。
もし適切に保護されていない場合、攻撃者は攻撃のためカーネルモジュールを悪用できてしまいます。

## どのように役に立つのでしょうか

eBPFはユーザー定義プログラムの実行環境として、Linuxカーネルモジュールよりも制御、制限された環境を提供します。
eBPFプログラムはカーネル内のサンドボックス化された環境で動作することで、隔離を提供しリスクを低減します。
もしeBPFプログラム中の脆弱性や欠陥が悪用されたとしても、一般的にその影響はサンドボックス化された環境に抑えられます。
さらに、eBPFプログラムがカーネル内で動作を開始する前に、プログラムはいくつかの検証を通る必要があります。
検証器は、範囲外メモリーアクセス、無限ループや承認されていないカーネル関数の使用といった潜在的な安全違反がないかeBPFプログラムを確認します。
このようにして、プログラムが無限ループに入り、カーネルをクラッシュさせないことを確かにします。
これらの安全制御によって、Linuxカーネル内でアプリケーションを動かすための選択肢としてeBPFはLinuxカーネルモジュールよりも安全なものになっています。
