# AdGuard DNS filter (without privacy filters)

A DNS filter that removed tracking and privacy rules from AdGuard DNS filter.  
This filter blocks only ad domains.

このフィルタは、AdGuard DNSフィルタからトラッキングやプライバシー用のブロックルールを取り除いた、広告ブロック専用のDNSフィルターです。

AdGuard DNSフィルタは`configuration.json`ファイルに定義されている複数のドメインリストを合成して作られているため、configuration.json ファイルを編集することで、特定のフィルタのドメインリストを除いたAdGuard DNSフィルタをビルドすることができます。  
これを利用して、広告ブロックとは関係のないプライバシー系のフィルタのドメインリストを除外してAdGuard DNSフィルタをビルドしています。

オリジナルのAdGuard DNSフィルタから除外しているフィルタは以下の通りです。
* AdGuard Base filter cryptominers
* AdGuard Tracking Protection filter third-party trackers
* AdGuard Tracking Protection filter first-party trackers
* AdGuard Tracking Protection filter mobile trackers
* EasyPrivacy tracking servers
* EasyPrivacy third-party tracking servers
* EasyPrivacy international tracking servers
* EasyPrivacy third-party international tracking servers

また、Easylist Italyの広告サーバーリストがあるとなぜかビルドに失敗するため、これも除外しています。申し訳ございません。
* EasyList Italy ad servers

## 注意
もしかしたら、「トラッキングのドメインかと思われていてプライバシー用のフィルタに入っていたドメインが、実は広告のドメインだった」みたいなことがあるかもしれません。その場合、このフィルタではプライバシー用のフィルタは取り除いてしまっているので、ブロック漏れが発生することになります。
あくまでも、一つの完成されているフィルタの一部を欠損させているフィルタであるということに注意してください。

また、このフィルタについて何か問題があったら連絡ください。

Original readme:
https://github.com/AdguardTeam/AdGuardSDNSFilter#readme
