# AdGuard DNS filter without privacy filters (Ads only)
A DNS filter that removed tracking and privacy rules from AdGuard DNS filter.  
This filter blocks only ad domains.

### AdGuard DNSフィルタ（プライバシー抜き）
AdGuard DNSフィルタからトラッキングやプライバシー用のフィルタを取り除いてみたDNSフィルタです。追跡、解析等のブロックが不要な方向け。

## AdGuardで購読する
購読するには、AdGuardのDNSフィルタの設定で「＋DNSフィルタを追加」をタップし、下記のURLを指定します。  
https://raw.githubusercontent.com/kitadai31/AdGuardSDNSFilter_withoutPrivacyFilters/master/Filters/filter.txt

## 目的
本家のAdGuard DNSフィルタは、広告ブロック用のフィルタだけでなくプライバシー用のフィルタも一緒になっているため、「プライバシー用のフィルタは要らない」と思っていても、広告ブロック用のDNSフィルタだけを個別に購読することができません。

一方で、この「**AdGuard DNSフィルタ（プライバシー抜き）**」は本家のDNSフィルタからプライバシー専用のフィルタを抜いているので、AdGuardのDNSフィルタリングで広告のみをブロックできます。

そのため、Wikiや本スレで初心者向けに推奨されている、コンテンツブロックのフィルタ設定でプライバシーなどを切って「AdGuardベースフィルタ・AdGuardモバイル広告フィルタ・AdGuard日本語フィルタ」の三点セットで使う設定とも親和性が高いです。
> 注意: これはあくまでもフィルタ生成の段階でプライバシー用のフィルタを除外しただけなので、残ったフィルタにプライバシー向けなブロックルールが一部含まれていることは起こり得ます。

### 対象
・プライバシーフィルタが一緒になっているのは精神衛生上よくない  
・私は追跡やアクセス解析を許容する  
・なるべく広告だけをブロックしたい  
・広告じゃないのに余計なブロックが発生するのが嫌だ  
・ブロックを減らしたい

といったこだわりのある方向けです。

【つまりはあくまでもカスタマイズに慣れたユーザー向け】
---
ということにしておきます

なお軽量フィルタではありません。（「DNSフィルタリングでルール数によって重さが変わるのか？」という疑問はさておき、）280Blockerのフィルタと比較すると、2021/09/26時点で公式は40000ルール程度、プライバシー抜きは32060ルール、一方で280は1309ルールです。軽量が目的な人にはあまり関係のないフィルタです。  
(ちなみに、280にはプライバシールールは一部含まれています。)

### 誤爆防止
また、副次的な効果として誤爆が減ることもあるようです。  
具体例としては、`google-analytics.com`をブロックすると起動しないアプリ(実在するそうです)を使いたい場合、公式DNSフィルタではブロックされてしまうため起動しませんが、プライバシー抜きならブロックされないので起動できます。これは、抜いているプライバシーフィルタの中に`||google-analytics.com^`というルールがあるためです。google-analytics.comは広告ではないので、アクセス解析のブロックが不要な人にとっては必要のないルールです。

追跡や解析ブロックが不要な人にとっては、プライバシー関連の不要なルールがないことで公式と比べると無駄な誤爆を減らすことができます。  
(google-analytics.comをブロックしたくないだけなら、DNSのユーザーフィルタに`@@||google-analytics.com^`を追加する方法もありますが。)

## 仕組み
そもそも公式のAdGuard DNSフィルタは、各種フィルタをスクリプトで機械的に合成・DNS用に調整し、自動で生成(ビルド)されているものになっています。(これは[公式GitHub](https://github.com/AdguardTeam/AdGuardSDNSFilter)で公開されています。このリポジトリはこれのフォークです)

このとき合成される各フィルタは`configuration.json`ファイルに定義されています。  
プライバシー抜きフィルタは、この`configuration.json`ファイルを編集してビルド時にプライバシー用のフィルタを除外する、という仕組みでできています。  
つまり、フィルタの生成の仕組みやスクリプトは公式とほぼ同じです。

公式DNSフィルタの`configuration.json`から除外しているフィルタ(のファイル)は以下の通りです。
* AdGuard Base filter cryptominers
* AdGuard Tracking Protection filter third-party trackers
* AdGuard Tracking Protection filter first-party trackers
* AdGuard Tracking Protection filter mobile trackers
* EasyPrivacy tracking servers
* EasyPrivacy third-party tracking servers
* EasyPrivacy international tracking servers
* EasyPrivacy third-party international tracking servers

要するに、公式DNSフィルタで合成されているフィルタから「AdGuard追跡防止フィルタ」「EasyPrivacy」「EasyList Italy」「AdGuardベースフィルタのうちの暗号通貨マイニングフィルタ」の4つを除外してビルドしているということです。

また、フィルタはGitHub Actionsにより自動で毎日4:24にビルド(更新)されます。

ちなみに、ビルド時に除外している「AdGuard追跡防止フィルタ」「EasyPrivacy」は完全にプライバシー専用のフィルタとして設計されています。ですので「公式のDNSフィルタでは発生しない広告のブロック漏れが『プライバシー抜き』の方では発生してしまう」ということは起こらない　はず　です。  
しかし、何らかの間違いによって公式では発生しないブロック漏れが起こるかもしれません。「プライバシー抜き」は、あくまでも一つの完成されたフィルタの一部を改変しているフィルタであるということに留意して使用してください。
