---
layout: page
permalink: /en/compatibility/blocksettle/

name: BlockSettle
internal_url: /en/compatibility/blocksettle
logo: /img/compatibility/blocksettle/blocksettle.png
rbf:
  tested:
    date: "2020-10-29"
    platforms:
      - Linux
    version: "0.91.1"
  features:
    receive:
      notification: "true"
      list: "true"
      details: "true"
      shows_replaced_version: "true"
      shows_original_version: "false"
    send:
      signals_bip125: "true"
      list: "true"
      details: "false"
      shows_replaced_version: "true"
      shows_original_version: "false"
  examples:
    - image: /img/compatibility/blocksettle/rbf/RBF_desktop_notification.png
      caption: >
        Desktop notification includes RBF signaling
    - image: /img/compatibility/blocksettle/rbf/RBF_txdetail_signalling.png
      caption: >
        Transaction details includes RBF signaling
    - image: /img/compatibility/blocksettle/rbf/RBF_txlist_signalling.png
      caption: >
        Transaction List includes RBF signaling
    - image: /img/compatibility/blocksettle/rbf/RBF_txlist_replacement.png
      caption: >
        The transaction list displays the new incoming transaction, as well as the
        new outgoing transaction
    - image: /img/compatibility/blocksettle/rbf/RBF_txoverview.png
      caption: >
        The transaction overview includes RBF signaling
    - image: /img/compatibility/blocksettle/rbf/RBF_txdetails_send.png
      caption: >
        The transactions details include RBF signaling
    - image: /img/compatibility/blocksettle/rbf/RBF_default_check.png
      caption: >
        The create transaction dialog has RBF signaling enabled by default
    - image: /img/compatibility/blocksettle/rbf/RBF_right_click.png
      caption: >
        The RBF function can be selected by right-clicking on an RBF eligible transaction
    - image: /img/compatibility/blocksettle/rbf/RBF_default_outputs.png
      caption: >
        The RBF dialog pre-populates the existing output by default
    - image: /img/compatibility/blocksettle/rbf/RBF_change_outputs.png
      caption: >
        The RBF dialog allows the user to replace/change/remove the output(s)
        to create a new transaction
segwit:
  tested:
    date: "2020-10-29"
    platforms:
      - Linux
    version: "0.91.1"
  features:
    receive:
      p2sh_wrapped: "true"
      bech32: "true"
      bech32m: "untested"
      default: "bech32"
    send:
      bech32: "true"
      bech32m: "untested"
      change_bech32: "true"
      segwit_v1: "Error message during broadcasting of transaction"
      bech32_p2wsh: "true"
  examples:
    - image: /img/compatibility/blocksettle/segwit/SegWit_wallet_overview.png
      caption: >
        The BlockSettle Terminal supports all address types. Users may hold/view/operate
        multiple wallets and can select the address type they wish to generate.
        The overview displays all wallets, address paths, and addresses.
    - image: /img/compatibility/blocksettle/segwit/SegWit_default.png
      caption: >
        The BlockSettle Terminal defaults to native bech32 segwit when the user
        generates an address.
    - image: /img/compatibility/blocksettle/segwit/SegWit_generate.png
      caption: >
        The BlockSettle Terminal displays the generated native bech32 segwit address
    - image: /img/compatibility/blocksettle/segwit/SegWit_send.png
      caption: >
        The BlockSettle terminal can send to native bech32 segwit addresses
    - image: /img/compatibility/blocksettle/segwit/SegWit_change.png
      caption: >
        The change address defaults to native bech32 segwit addresses, however,
        it is manually selectable by the user
---

<!-- BlockSettle -->

{% assign tool = page %}
{% include templates/compatibility-page.md %}
