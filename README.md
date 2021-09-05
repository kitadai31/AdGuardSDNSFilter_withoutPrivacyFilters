# AdGuard DNS filter (Ad servers only)

A DNS filter that removes tracking and privacy rules from AdGuard DNS filter.
This filter blocks only ad domains.
このフィルタは、AdGuard DNSフィルタからトラッキングとプライバシー用のブロックルールを取り除いた、広告ブロック専用のDNSフィルターです。

AdGuard DNSフィルタは configuration.json ファイルに定義されている複数のフィルタの広告サーバーのリストを合成して作られているため、configuration.json ファイルを編集することで特定のフィルタを除いたAdGuard DNSフィルタをビルドすることができます。
これを利用して、広告ブロックとは関係のないプライバシー関係のルールを取り除いたフィルタをビルドしています。

オリジナルのAdGuard DNSフィルタから取り除いているフィルタは以下の通りです。
* AdGuard Base filter cryptominers
* AdGuard Tracking Protection filter third-party trackers
* AdGuard Tracking Protection filter first-party trackers
* AdGuard Tracking Protection filter mobile trackers
* EasyPrivacy tracking servers
* EasyPrivacy third-party tracking servers
* EasyPrivacy international tracking servers
* EasyPrivacy third-party international tracking servers

## 注意
もしかしたら、「トラッキングのドメインかと思われていてプライバシー用のフィルタに入っていたドメインが、実は広告のドメインだった」みたいなことがあるかもしれません。その場合、このフィルタではプライバシー用のフィルタは取り除いてしまっているので、オリジナルのフィルタでは発生しないブロック漏れが発生することになります。
あくまでも、一つの完成されているフィルタの一部を欠損させているフィルタであるということに注意してください。

また、このフィルタについて何か問題があったら連絡ください。


The original readme below:

Formerly *AdGuard Simplified Domain names filter*.

A filter composed of several other filters (AdGuard Base filter, Social media filter, Tracking Protection filter, Mobile Ads filter, EasyList and EasyPrivacy) and simplified specifically to be better compatible with DNS-level ad blocking.

The direct link to the filter: https://adguardteam.github.io/AdGuardSDNSFilter/Filters/filter.txt.

Please note, that to use this filter it is necessary to support [basic ad blocking rules syntax](https://kb.adguard.com/en/general/how-to-create-your-own-ad-filters). It does not make much sense to extract just the hosts file.

This is a default filter for [AdGuard Home](https://github.com/AdguardTeam/AdGuardHome) and for the public [AdGuard DNS](https://adguard.com/en/adguard-dns/overview.html) servers.

### How to build AdGuard DNS filter manually

```
yarn install
yarn run build
```

The output is written to `Filters/filter.txt`.
