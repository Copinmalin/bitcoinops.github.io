---
layout: page
permalink: /en/compatibility/jaxx/

name: Jaxx
internal_url: /en/compatibility/jaxx
logo: /img/compatibility/jaxx/jaxx.png
rbf:
  tested:
    date: "2018-11-07"
    platforms:
      - iOS
    version: "2.0.5"
  features:
    receive:
      notification: "na"
      list: "false"
      details: "false"
      shows_replaced_version: "true"
      shows_original_version: "false"
    send:
      signals_bip125: "false"
      list: "untested"
      details: "untested"
      shows_replaced_version: "untested"
      shows_original_version: "untested"
  examples:
    - image: /img/compatibility/jaxx/rbf/transaction-list-incoming-rbf.png
      caption: >
        Receiving Transaction Signaling RBF - Transaction list showing incoming transaction. RBF not noted.
    - image: /img/compatibility/jaxx/rbf/transaction-list-incoming-replacement.png
      caption: >
        Receiving Replacement Transaction - Replacement transaction shown, original disappears.
segwit:
  tested:
    date: "2019-07-24"
    platforms:
      - iOS
    version: "2.2.2"
  features:
    receive:
      p2sh_wrapped: "false"
      bech32: "false"
      bech32m: "untested"
      default: "p2pkh"
    send:
      bech32: "false"
      bech32m: "untested"
      change_bech32: "false"
      segwit_v1: "Fails on validation of the address."
      bech32_p2wsh: "false"
  examples:
    - image: /img/compatibility/jaxx/segwit/receive-screen.png
      caption: >
        Jaxx generates only legacy P2PKH receive addresses.
    - image: /img/compatibility/jaxx/segwit/send-screen.png
      caption: >
        Jaxx cannot send to any bech32 addresses.
    #- image: /img/compatibility/jaxx/segwit/send-screen-segwit-v1-error.png
    #  caption: >
    #    Jaxx displays a validation error when trying to send to a segwit v1
    #    address (or any other bech32 address).
---

<!-- Jaxx -->

{% assign tool = page %}
{% include templates/compatibility-page.md %}
