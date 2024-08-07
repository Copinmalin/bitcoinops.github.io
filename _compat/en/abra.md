---
layout: page
permalink: /en/compatibility/abra/

name: Abra
internal_url: /en/compatibility/abra
logo: /img/compatibility/abra/abra.png
rbf:
  tested:
    date: "2018-12-06"
    platforms:
      - iOS
    version: "5.4.0"
  features:
    receive:
      notification: "na"
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
    - image: /img/compatibility/abra/rbf/send-screen-default.png
      caption: >
        Sending Transaction - Default send transaction screen.
    - image: /img/compatibility/abra/rbf/send-confirm.png
      caption: >
        Sending Transaction - Send transaction confirmation screen.
    - image: /img/compatibility/abra/rbf/send-fee-notice.png
      caption: >
        Sending Transaction - Network fee notice details.
    - image: /img/compatibility/abra/rbf/transaction-list-sent.png
      caption: >
        Sending Transaction - Transaction list screen showing sent transaction. No RBF notice.
    - image: /img/compatibility/abra/rbf/transaction-details-sent.png
      caption: >
        Sending Transaction - Sent transaction details. No RBF notice. Note transaction sent without RBF flag. Transaction was not sent with RBF so no bumping available.
    - image: /img/compatibility/abra/rbf/transaction-list-incoming-rbf.png
      caption: >
        Receiving Transaction Signaling RBF - Abra does not show unconfirmed transactions.
    - image: /img/compatibility/abra/rbf/notification-incoming-replacement.png
      caption: >
        Receiving Replacement Transaction - When the replacement transaction receives 1 confirmation it appears in wallet. No RBF notice.
    - image: /img/compatibility/abra/rbf/transaction-list-incoming-replacement.png
      caption: >
        Receiving Replacement Transaction - Transaction list screen. No RBF flag.
    - image: /img/compatibility/abra/rbf/transaction-details-replacement-confirmed.png
      caption: >
        Receiving Replacement Transaction - Replacement transaction details.
segwit:
  tested:
    date: "2019-04-11"
    platforms:
      - iOS
    version: "5.11.1"
  features:
    receive:
      p2sh_wrapped: "false"
      bech32: "false"
      bech32m: "untested"
      default: "p2pkh"
    send:
      bech32: "false"
      bech32m: "untested"
      change_bech32: "untested"
      segwit_v1: "Bech32 not supported."
      bech32_p2wsh: "false"
  examples:
    - image: /img/compatibility/abra/segwit/receive-screen.png
      caption: >
        Abra uses P2PKH addresses for receiving.
    - image: /img/compatibility/abra/segwit/send-bech32.png
      caption: >
        Abra allows a bech32 address to be input and does not provide a warning.
        However, the review button was not enabled until a non-bech32 address
        was provided. The eventually sent transaction used exact change so
        change address format was not determined.
    - image: /img/compatibility/abra/segwit/send-bech32-qr.png
      caption: >
        When using the QR code scanner, an error about address format was shown
        when scanning a bech32 address.
    - image: /img/compatibility/abra/segwit/send-non-bech32.png
      caption: >
        When using a non bech32 address, the "Review" button is enabled. Button
        is disabled when using bech32 address format.
---

<!-- Abra -->

{% assign tool = page %}
{% include templates/compatibility-page.md %}
