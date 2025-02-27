---
aliases:
- /ja/tracing/compatibility_requirements/php
- /ja/tracing/setup_overview/compatibility_requirements/php
code_lang: php
code_lang_weight: 50
description: PHP トレーサーの互換性要件です
further_reading:
- link: tracing/trace_collection/dd_libraries/php
  tag: ドキュメント
  text: アプリケーションのインスツルメンテーション
kind: documentation
title: PHP 互換性要件
type: multi-code-lang
---
## PHP APM のランタイムサポートポリシー

PHP Datadog Trace ライブラリはオープンソースです。詳細については、[GitHub リポジトリ][1]をご覧ください。

Datadog APM for PHP は、ホスト OS や PHP ランタイム、特定の PHP ライブラリ、 Datadog Agent や API の特定のバージョンで定義される依存関係に基づいて構築されています。
これらのバージョンがメンテナによってサポートされなくなった場合、 Datadog APM for PHP はこれらのサポートにも制限をかけます。

#### サポートレベル

| **レベル**                                              | **サポート内容**                                                                                                                                                          |
|--------------------------------------------------------|-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| <span id="support-unsupported">非対応</span>      |  実装していません。[特別なご要望はカスタマーサポートチームにお問い合わせください][2]。                                                             |
| <span id="support-beta">ベータ版</span>                    |  初期実装です。まだすべての機能が含まれていない可能性があります。新機能のサポート、バグやセキュリティの修正は、ベストエフォートで提供されます。                                    |
| <span id="support-ga">一般提供 (GA)</span> |  全機能の完全実装。新機能、バグ、セキュリティフィックスを完全サポート。                                                                                    |
| <span id="support-maintenance">メンテナンス</span>      |  既存機能の完全実装。新機能は受けません。バグフィックス、セキュリティフィックスのみの対応となります。                                                              |
| <span id="support-legacy">レガシー</span>                |  レガシーな実装。機能は限定されますが、メンテナンスは提供されません。[特別なご要望がある場合は、サポートチームにお問い合わせください。 |
| <span id="support-eol">サポート終了 (EOL)</span>        |  サポートなし。このバージョンはまだ使用可能ですが、バグ修正は提供されません。                                                                                                  |


PHP APM は以下のバージョンの PHP (ZTS と NTS の両方) に対応しています。

<div class="alert alert-info">
<strong>注:</strong>
PHP 5.x はバージョン 0.75.0 まで完全にサポートされています。現在はメンテナンスモードに移行しており、2023 年 12 月 31 日までセキュリティや重要なバグの修正でサポートされています。
<br>
もし、アプリケーションで PHP 5.x バージョンを使用していて、ビジネスニーズにとって重要な機能要求がある場合は、<a href="https://www.datadoghq.com/support/">Datadog サポート</a>にご連絡ください。
<br>
PHP は公式にサポートされているバージョン、特に 7.4、8.0、8.1 を使用することが推奨されています。
</div>

| PHP バージョン    | サポートレベル                         | パッケージバージョン |
|:---------------|:--------------------------------------|:----------------|
| 8.2.x          | 一般提供                  | > `0.82.0+`     |
| 8.1.x          | 一般提供                  | > `0.66.0+`     |
| 8.0.x          | 一般提供                  | > `0.52.0+`     |
| 7.4.x          | 一般提供                  | すべて             |
| 7.3.x          | 一般提供                  | すべて             |
| 7.2.x          | 一般提供                  | すべて             |
| 7.1.x          | 一般提供                  | すべて             |
| 7.0.x          | 一般提供                  | すべて             |
| 5.6.x          | メンテナンス (2023 年 12 月 31 日まで) | すべて             |
| 5.5.x          | メンテナンス (2023 年 12 月 31 日まで) | すべて             |
| 5.4.x          | メンテナンス (2023 年 12 月 31 日まで) | すべて             |

PHP APM は以下の SAPI に対応しています。

| SAPI           | サポートの種類    |
|:---------------|:----------------|
| apache2handler | 完全対応 |
| cli            | 完全対応 |
| fpm-fcgi       | 完全対応 |
| cgi-fcgi       | 完全対応 |

## 対応プロセッサアーキテクチャー

PHP APM は以下のアーキテクチャに対応しています。

| プロセッサアーキテクチャー                   | サポートレベル         | パッケージバージョン                        |
| ------------------------------------------|-----------------------|----------------------------------------|
| Linux GNU amd64 (`x86-64-linux-gnu`)      | [GA](#support-ga)     | すべて                                    |
| Linux MUSL amd64 (`x86-64-linux-musl`)    | [GA](#support-ga)     | すべて                                    |
| Linux GNU arm64 (`aarch64-linux-gnu`)     | [GA](#support-ga)     | > `0.78.0`                             |
| Linux MUSL arm64 (`aarch64-linux-musl`)   | [GA](#support-ga)     | > `0.78.0`                             |

### インテグレーション

#### Web フレームワークの互換性

Datadog はデフォルトで、**すべての PHP Web フレームワークをサポート**し、フレームワークレベルのインスツルメンテーション、または一般的な Web トレースを行うことができます。

フレームワークレベルのインスツルメンテーションには、内部メソッドのトレースとフレームワーク固有のタグ付けが含まれます。

一般的な Web トレースには、データベースや HTTP クライアントなどのサポートされたライブラリのスパンに加えて、コールから発生したレイテンシーやエラーを追跡するための `web.request` スパンが含まれています。

次の表は、Datadog が正常にトレースするフレームワークとバージョンの一部を示しています。

**ウェブフレームワーク**:

| モジュール         | バージョン             | サポートの種類               | インスツルメンテーションレベル           |
|:-------------- |:---------------------|:---------------------------|:--------------------------------|
| CakePHP        | 2.x                  | サポートされているすべての PHP バージョン | フレームワークレベルのインスツルメンテーション |
| CodeIgniter    | 2.x                  | PHP 7+                     | フレームワークレベルのインスツルメンテーション |
| CodeIgniter    | 3.x                  | PHP 7+                     | 一般的な Web トレース             |
| Drupal         |                      | サポートされているすべての PHP バージョン | 一般的な Web トレース             |
| FuelPHP        | 1.1                  | PHP 7+                     | 一般的な Web トレース             |
| Laminas        |                      | サポートされているすべての PHP バージョン | フレームワークレベルのインスツルメンテーション |     
| Laravel        | 4.2、5.x、6.x        | サポートされているすべての PHP バージョン | フレームワークレベルのインスツルメンテーション |
| Laravel 8      | 8.x (トレーサー `0.52.0+`) | サポートされているすべての PHP バージョン | フレームワークレベルのインスツルメンテーション |
| Lumen          |   5.2+                 | サポートされているすべての PHP バージョン | フレームワークレベルのインスツルメンテーション |
| Magento        | 1、2                 | サポートされているすべての PHP バージョン | 一般的な Web トレース             |
| Neos Flow      | 1.1                  | サポートされているすべての PHP バージョン | 一般的な Web トレース             |
| Phalcon        | 1.3、3.4             | サポートされているすべての PHP バージョン | 一般的な Web トレース             |
| RoadRunner     | 2.x                  | サポートされているすべての PHP バージョン | フレームワークレベルのインスツルメンテーション |
| Slim           | 2.x、3.x、4.x        | サポートされているすべての PHP バージョン | フレームワークレベルのインスツルメンテーション |
| Symfony        | 2.x、3.3、3.4、4.x、5.x、6.x | サポートされているすべての PHP バージョン | フレームワークレベルのインスツルメンテーション |
| WordPress      | 4.x、5.x             | PHP 7+                     | フレームワークレベルのインスツルメンテーション |
| Yii            | 1.1、2.0             | サポートされているすべての PHP バージョン | フレームワークレベルのインスツルメンテーション |
| Zend Framework | 1.12、1.21           | サポートされているすべての PHP バージョン | フレームワークレベルのインスツルメンテーション |
| Zend Framework | 2.x                  | サポートされているすべての PHP バージョン | 一般的な Web トレース             |

このリストにウェブフレームワークがない場合でも、トレーサーの最新リリースではそのまま使用できます。

Datadog では、PHP ウェブフレームワークのより詳細なトレースのためのサポートを継続的に追加しています。スパンメタデータおよびフレームワーク内部に対するさらなるサポートをご希望の場合は、[サポートチーム][3]までお気軽にお問い合わせください。

#### CLI ライブラリの互換性

デフォルトで、CLI SAPI からのトレースは無効になっています。PHP CLI スクリプトのトレースを有効にするには、`DD_TRACE_CLI_ENABLED=true` とします。

| モジュール          | バージョン | サポートの種類    |
|:----------------|:---------|:----------------|
| CakePHP Console | 2.x      | 完全対応 |
| Laravel Artisan | 5.x、8.x | 完全対応 |
| Symfony CLI     | 4.x、5.x、6.x | 完全対応 |

追加 CLI ライブラリに関するサポートをご希望の場合は、[サポートチーム][3]までお気軽にお問い合わせください。

#### データストアの互換性

| モジュール                                                                  | バージョン                   | サポートの種類    |
|-------------------------------------------------------------------------|----------------------------|-----------------|
| Amazon RDS (PDO または MySQLi 使用)                                        | *(対応する PHP)*      | 完全対応 |
| Elasticsearch                                                           | 1+                         | 完全対応 |
| Eloquent                                                                | Laravel 対応バージョン | 完全対応 |
| Laravel キュー                                                          | Laravel 対応バージョン | 完全対応 |
| Memcache                                                                | *(対応する PHP)*      | 完全対応 |
| Memcached                                                               | *(対応する PHP)*      | 完全対応 |
| MongoDB - [mongo][4] 拡張機能を使用                                      | 1.4.x                      | 完全対応 |
| MySQLi                                                                  | *(対応する PHP)*      | 完全対応 |
| PDO                                                                     | *(対応する PHP)*      | 完全対応 |
| PhpRedis                                                                | 3、4、5                    | PHP 7、8        |
| Predis                                                                  | 1.1                        | 完全対応 |
| SQLSRV                                                                  | *(対応する PHP)*      | 完全対応 |

追加データストアに関するサポートをご希望の場合は、[サポートチーム][3]までお気軽にお問い合わせください。

#### ライブラリの互換性

| モジュール     | バージョン              | サポートの種類    |
|:-----------|:----------------------|:----------------|
| Amqp       | 2.x、3.x              | PHP 7.1+        |
| Curl       | *(対応する PHP)* | 完全対応 |
| Guzzle     | 5.x、6.x、7.x         | 完全対応 |


ライブラリに関するサポートをご希望の場合は、[サポートチーム][3]までお気軽にお問い合わせください。

#### PHP 5 の深いコールスタック

コールスタックは PHP 5 のみに限定されます。詳細は[深いコールスタックのトラブルシューティングページ][5]を参照してください。 

### ジェネレータ

[ジェネレータ][6]のインスツルメントは、PHP 5 および PHP 7 ではサポートされていません。

### PCNTL

Datadog は、[pcntl][7] を使ってフォークされたプロセスのトレースをサポートしています。`pcntl_fork` のコールが検出されると、専用のスパンが作成され、フォークされたプロセスがインスツルメントされます。これは `DD_TRACE_FORKED_PROCESS` で無効にすることができます。詳細については、[ライブラリの構成ページ][9]を参照してください。

アプリケーションが `pcntl_unshare(CLONE_NEWUSER);` を実行し、トレーサーがインストールされている場合、アプリケーションは致命的にクラッシュします。これは、`CLONE_NEWUSER` を持つ `unshare` がプロセスを[スレッド化しない][8]ことを要求し、PHP トレーサーが別スレッドを使用してメインプロセスをブロックせずに Datadog Agent にトレースを送信するために起こります。

## その他の参考資料

{{< partial name="whats-next/whats-next.html" >}}

[1]: https://github.com/DataDog/dd-trace-php
[2]: https://www.datadoghq.com/support/
[3]: /ja/help
[4]: https://pecl.php.net/package/mongo
[5]: /ja/tracing/troubleshooting/php_5_deep_call_stacks
[6]: https://www.php.net/manual/en/language.generators.overview.php
[7]: https://www.php.net/manual/en/book.pcntl.php
[8]: https://man7.org/linux/man-pages/man2/unshare.2.html
[9]: /ja/tracing/trace_collection/library_config/php/#environment-variable-configuration