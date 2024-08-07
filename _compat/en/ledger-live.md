---
layout: page
permalink: /en/compatibility/ledger-live/

name: Ledger Live
internal_url: /en/compatibility/ledger-live
logo: /img/compatibility/ledger-live/ledger-live.png
rbf:
  tested:
    date: "2018-10-11"
    platforms:
      - macOS
    version: "1.2.0"
  features:
    receive:
      notification: "false"
      list: "false"
      details: "false"
      shows_replaced_version: "false"
      shows_original_version: "true"
    send:
      signals_bip125: "false"
      list: "untested"
      details: "untested"
      shows_replaced_version: "untested"
      shows_original_version: "untested"
  examples:
    - image: /img/compatibility/ledger-live/rbf/send-screen.png
      caption: >
        Sending Transaction - Send transaction screen does not allow for RBF. Fee options are available. No RBF options in settings.
    - image: /img/compatibility/ledger-live/rbf/transaction-details-sent.png
      caption: >
        Attempting Transaction Replacement - Transaction details screen. No RBF fee bumping supported.
    - image: /img/compatibility/ledger-live/rbf/transaction-list-incoming-rbf.png
      caption: >
        Receiving Transaction Signaling RBF - Transaction list screen. No RBF flag.
    - image: /img/compatibility/ledger-live/rbf/transaction-details-incoming-rbf.png
      caption: >
        Receiving Transaction Signaling RBF - Transaction details screen. No RBF flag.
    - image: /img/compatibility/ledger-live/rbf/transaction-list-incoming-replacement.png
      caption: >
        Receiving Replacement Transaction - Transaction list screen does not show the replacement transaction. Only the original. Even after the new, replacement transaction received 6+ confirmations.
    - image: /img/compatibility/ledger-live/rbf/error-screen.png
      caption: >
        Receiving Transaction Signaling RBF - Internal database error shows conflicting
        bitcoin inputs. Original transaction remains unconfirmed. Ticket opened
        with Ledger to address. Update - Solution was to clear cache in app.
segwit:
  tested:
    date: "2019-07-24"
    platforms:
      - macOS
    version: "1.12.0"
  features:
    receive:
      p2sh_wrapped: "true"
      bech32: "true"
      bech32m: "true"
      default: "bech32"
    send:
      bech32: "true"
      bech32m: "true"
      change_bech32: "true"
      segwit_v1: "Fails when transaction is sent to the hardwave device for signing."
      bech32_p2wsh: "true"
  examples:
    - image: /img/compatibility/ledger-live/segwit/receive-screen.png
      caption: >
        Ledger Live can generate bech32 native addresses. Note this depends on
        how your wallet was initial created. Bech32 support is new in Ledger Live.
    - image: /img/compatibility/ledger-live/segwit/send-screen.png
      caption: >
        Ledger Live can send to all variants of bech32 addresses for v0.
    #- image: /img/compatibility/ledger-live/segwit/send-screen-segwit-v1-error.png
    #  caption: >
    #    Ledger Live displays an error during hardware device signing when trying
    #    to send to a segwit v1 address.
---

<!-- Ledger Live -->

{% assign tool = page %}
{% include templates/compatibility-page.md %}
