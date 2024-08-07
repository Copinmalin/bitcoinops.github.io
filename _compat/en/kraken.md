---
layout: page
permalink: /en/compatibility/kraken/

name: Kraken
internal_url: /en/compatibility/kraken
logo: /img/compatibility/kraken/kraken.png
rbf:
  tested:
    date: "2020-02-21"
    platforms:
      - web
    version: "n/a"
  features:
    receive:
      notification: "false"
      list: "false"
      details: "false"
      shows_replaced_version: "false"
      shows_original_version: "false"
    send:
      signals_bip125: "false"
      list: "untested"
      details: "untested"
      shows_replaced_version: "untested"
      shows_original_version: "untested"
  examples:
    - image: /img/compatibility/kraken/rbf/send-confirm.png
      caption: >
        Sending Transaction - Send confirmation screen. No RBF options.
        Transactions are not sent signaling RBF.
    - image: /img/compatibility/kraken/rbf/transaction-list.png
      caption: >
        Receiving Transaction Signaling RBF - No unconfirmed transactions appear
        in transaction list. No RBF note.
segwit:
  tested:
    date: "2020-02-21"
    platforms:
      - web
    version: "n/a"
  features:
    receive:
      p2sh_wrapped: "true"
      bech32: "false"
      bech32m: "false"
      default: "p2sh_wrapped_p2wsh"
    send:
      bech32: "true"
      bech32m: "true"
      change_bech32: "false"
      segwit_v1: ""
      bech32_p2wsh: "true"
  examples:
    - image: /img/compatibility/kraken/segwit/receive-screen.png
      caption: >
        Kraken receives deposits to P2SH-P2WSH addresses.
    - image: /img/compatibility/kraken/segwit/create-address.png
      caption: >
        Kraken can send to all variants of bech32 addresses for v0.
    - image: /img/compatibility/kraken/segwit/send-screen.png
      caption: >
        Default send screen.
---

<!-- Kraken -->

{% assign tool = page %}
{% include templates/compatibility-page.md %}
