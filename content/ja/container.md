---
title: コンテナ
status: Completed
category: テクノロジー
tags: ["アプリケーション", "基礎", ""]
---

コンテナは、コンピューターのオペレーティングシステムがリソースと機能面での制限を管理する、実行中のプロセスです。
コンテナプロセスで利用可能なファイルは、コンテナイメージとしてパッケージ化されています。
コンテナは一つのマシン上で同時に実行されますが、通常オペレーティングシステムは別々のコンテナプロセスが互いに干渉するのを防ぎます。

## 解決すべき問題は何ですか

コンテナが利用可能になる前は、アプリケーションを実行するためには別々のマシンが必要でした。
各マシンはそれぞれのオペレーティングシステムを必要とし、CPU、メモリ、ディスクスペースを消費します。
これらは全て個々のアプリケーションが動作するために必要なものです。
さらに、オペレーティングシステムのメンテナンス、アップグレード、起動は大きな手間のかかる作業です。

## どのように役に立つのでしょうか

コンテナはオペレーティングシステムとそのマシンリソースを共有し、オペレーティングシステムのリソースオーバーヘッドを分散させ、物理マシンを効率的に使用します。
これは通常コンテナが互いに干渉することが制限されているため、実現できます。
これにより、同じ物理マシン上で多くのアプリケーションを実行することができます。

しかし、いくつかの制限もあります。
コンテナは同じオペレーティングシステムを共有するため、プロセスは代替手段と比べて安全性が低いと考えられます。
またコンテナは、共有されるリソースへの制限を必要とします。
リソースを保証するために、管理者はメモリやCPUの使用を制限し、他のアプリケーションのパフォーマンスが低下しないようにする必要があります。
