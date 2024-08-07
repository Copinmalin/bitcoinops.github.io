---
layout: page
permalink: /en/compatibility/greenaddress/

name: Green
internal_url: /en/compatibility/greenaddress
logo: /img/compatibility/greenaddress/greenaddress.png
rbf:
  tested:
    date: "2018-09-25"
    platforms:
      - iOS
    version: "0.0.52"
  features:
    receive:
      notification: "na"
      list: "true"
      details: "false"
      shows_replaced_version: "true"
      shows_original_version: "true"
    send:
      signals_bip125: "true"
      list: "true"
      details: "false"
      shows_replaced_version: "true"
      shows_original_version: "true"
  examples:
    - image: /img/compatibility/greenaddress/rbf/settings-transaction-replacement.png
      caption: >
        Sending Transaction - Sending with transaction replacement is “ON” under Settings by default.
    - image: /img/compatibility/greenaddress/rbf/default-send-transaction-screen.png
      caption: >
        Sending Transaction - Default Send transaction screen.
    - image: /img/compatibility/greenaddress/rbf/send-transaction-screen-advanced.png
      caption: >
        Sending Transaction - Advanced details on send transaction screen.
    - image: /img/compatibility/greenaddress/rbf/transaction-send-confirmation-prompt.png
      caption: >
        Sending Transaction - Transaction send confirmation prompt.
    - image: /img/compatibility/greenaddress/rbf/transaction-list-bump-fee.png
      caption: >
        Sending Transaction - Transaction list showing “bump fee” option for unconfirmed transaction.
    - image: /img/compatibility/greenaddress/rbf/sent-transaction-details.png
      caption: >
        Sending Transaction - Transaction details. RBF replaceable not flagged.
    - image: /img/compatibility/greenaddress/rbf/transaction-list-bump-fee-context-menu.png
      caption: >
        Attempting Transaction Replacement - Bump fee context menu options.
    - image: /img/compatibility/greenaddress/rbf/replacement-transaction-details.png
      caption: >
        Attempting Transaction Replacement - Bump transaction details confirmation. Notes “Previous fee:” field as well as language about bumping.
    - image: /img/compatibility/greenaddress/rbf/2fa-prompt.png
      caption: >
        Attempting Transaction Replacement - 2FA prompted for replacement transactions as well.
    - image: /img/compatibility/greenaddress/rbf/transaction-list-replacement-tx.png
      caption: >
        Attempting Transaction Replacement - Transaction list with replacement transaction on top. Bump fee available again. Show replaced transaction button shows as well.
    - image: /img/compatibility/greenaddress/rbf/transaction-list-show-replaced.png
      caption: >
        Attempting Transaction Replacement - Transaction list with replacement transactions “show replaced” button clicked. NOTE while testing, I inadvertently bumped twice so 2 replacement transactions appear here.
    - image: /img/compatibility/greenaddress/rbf/transaction-details-original-tx.png
      caption: >
        Attempting Transaction Replacement - Original transaction as viewed from the “show replaced” list. “Double spend by txhash” field has “update” value.
    - image: /img/compatibility/greenaddress/rbf/transaction-details-replacement-tx.png
      caption: >
        Attempting Transaction Replacement - Replacement “bumped” transaction. “Double spend by txhash” field has “update” value.
    - image: /img/compatibility/greenaddress/rbf/transaction-list-subsequent-replacement-fees.png
      caption: >
        Attempting Transaction Replacement - Subsequent bumping on the same transaction has a different “bump fee” context menu options. Also the context menu notes “fee already at 1-conf-estimate level”.
    - image: /img/compatibility/greenaddress/rbf/transaction-list-rbf-incoming.png
      caption: >
        Receiving Transaction Signaling RBF - Transaction List Screen. “Replaceable” noted.
    - image: /img/compatibility/greenaddress/rbf/transaction-details-rbf-incoming-1.png
      caption: >
        Receiving Transaction Signaling RBF - Transaction details do not flag RBF (or unconfirmed).
    - image: /img/compatibility/greenaddress/rbf/transaction-details-rbf-incoming-2.png
      caption: >
        Receiving Transaction Signaling RBF - Transaction details do not flag RBF (or unconfirmed).
    - image: /img/compatibility/greenaddress/rbf/transaction-list-incoming-replacement-tx.png
      caption: >
        Receiving Replacement Transaction - Transaction List Screen. Notes RBF(“replaceable”) transaction as well as double spend transaction. The replacement transaction also shows up as separate.
    - image: /img/compatibility/greenaddress/rbf/transaction-details-incoming-replacement-tx-1.png
      caption: >
        Receiving Replacement Transaction - Transaction details for replacement transaction. No RBF note or double spend note. Does show “double spend by txhash” field which points to original transaction.
    - image: /img/compatibility/greenaddress/rbf/transaction-details-incoming-replacement-tx-2.png
      caption: >
        Receiving Replacement Transaction - Transaction details for replacement transaction. No RBF note or double spend note. Does show “double spend by txhash” field which points to original transaction.
    - image: /img/compatibility/greenaddress/rbf/transaction-details-incoming-original-tx-1.png
      caption: >
        Receiving Replacement Transaction - Transaction details for original
        transaction. No RBF note or double spend note. Does show “double spend
        by txhash” field which points to new replacement transaction.
    - image: /img/compatibility/greenaddress/rbf/transaction-details-incoming-original-tx-2.png
      caption: >
        Receiving Replacement Transaction - Transaction details for original
        transaction. No RBF note or double spend note. Does show “double spend
        by txhash” field which points to new replacement transaction.
    - image: /img/compatibility/greenaddress/rbf/transaction-list-replacement-confirmed.png
      caption: >
        Receiving Replacement Transaction - Transaction list after the replacement transaction confirms. “Original” transaction doesn’t appear.
    - image: /img/compatibility/greenaddress/rbf/transaction-details-bumped-confirmed-tx.png
      caption: >
        Receiving Replacement Transaction - Transaction details for confirmed, replacement transaction. No note of double spend or RBF. “double spend by txhash” field disappears.
segwit:
  tested:
    date: "2019-07-24"
    platforms:
      - iOS
    version: "3.1.8"
  features:
    receive:
      p2sh_wrapped: "true"
      bech32: "false"
      bech32m: "untested"
      default: "p2sh_wrapped"
    send:
      bech32: "true"
      bech32m: "untested"
      change_bech32: "false"
      segwit_v1: "Fails on validation of the address."
      bech32_p2wsh: "true"
  examples:
    - image: /img/compatibility/greenaddress/segwit/receive-screen.png
      caption: >
        Green generates only P2SH wrapped segwit addresses.
    - image: /img/compatibility/greenaddress/segwit/send-screen.png
      caption: >
        Green can send to all variants of bech32 addresses for v0.
    #- image: /img/compatibility/greenaddress/segwit/send-screen-segwit-v1-error.png
    #  caption: >
    #    Green displays a validation error when trying to send to a segwit v1 address.
---

<!-- GreenAddress -->

{% assign tool = page %}
{% include templates/compatibility-page.md %}
