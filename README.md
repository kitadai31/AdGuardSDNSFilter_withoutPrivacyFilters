# AdGuard DNS filter without privacy filters (Ads only)
A DNS filter that removed tracking and privacy rules from AdGuard DNS filter.  
This filter blocks only ad domains.

このフィルタは、AdGuard DNSフィルタからトラッキングやプライバシー用のブロックルールを取り除いた、広告ブロック専用のDNSフィルタです。  

## AdGuardで購読する
購読するには、AdGuardのDNSフィルタの設定で「＋DNSフィルタを追加」をタップし、下記のURLを指定します。  
https://raw.githubusercontent.com/kitadai31/AdGuardSDNSFilter_withoutPrivacyFilters/master/Filters/filter.txt

## 概要
AdGuard DNSフィルタは、AdGuard Base filter, Social media filter, Tracking Protection filter, Mobile Ads filter, EasyList, EasyPrivacy などの複数のフィルタを合体して、DNS用に調整したものになっています。  
しかしそのため、プライバシー用のフィルタは要らない、という場合でも、広告ブロック用のDNSフィルタだけを個別に購読することができません。

ですが、AdGuard DNSフィルタは`configuration.json`ファイルに定義されている各フィルタのドメインリストを参照することで自動生成されているため、`configuration.json`ファイルを編集することで、特定のフィルタのドメインリストを除いたAdGuard DNSフィルタをビルドすることができます。  

このフィルタは、これを利用して、広告ブロックとは関係のないプライバシー系のフィルタを除外してAdGuard DNSフィルタをビルドしたものです。

オリジナルのAdGuard DNSフィルタから除外しているフィルタは以下の通りです。
* AdGuard Base filter cryptominers
* AdGuard Tracking Protection filter third-party trackers
* AdGuard Tracking Protection filter first-party trackers
* AdGuard Tracking Protection filter mobile trackers
* EasyPrivacy tracking servers
* EasyPrivacy third-party tracking servers
* EasyPrivacy international tracking servers
* EasyPrivacy third-party international tracking servers

また、Easylist Italyの広告サーバーリストがあるとなぜかビルドが失敗するため、除外しています。
* EasyList Italy ad servers

## 注意
もし「トラッキングのドメインとしてプライバシー用のフィルタに入っていたドメインが、実は広告のドメインだった」みたいなことがあった場合、このフィルタではプライバシー用のフィルタは取り除いてしまっているので、ブロック漏れが発生することになります。  
あくまでもこれは一つの完成されたフィルタの一部を欠損させているフィルタなので、元フィルタでは発生しないブロック漏れも起こるかもしれません。

Original readme:
https://github.com/AdguardTeam/AdGuardSDNSFilter#readme
