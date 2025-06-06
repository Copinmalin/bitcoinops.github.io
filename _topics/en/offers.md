---
title: Offers

## Optional.  Shorter name to use for reference style links e.g., "foo"
## will allow using the link [topic foo][].  Not case sensitive
# shortname: foo

## Optional.  An entry will be added to the topics index for each alias
title-aliases:
  - BOLT12

## Required.  At least one category to which this topic belongs.  See
## schema for options
topic-categories:
  - Lightning Network
  - Invoicing
  - Wallet Collaboration Tools

## Required.  Use Markdown formatting.  Only one paragraph.  No links allowed.
## Should be less than 500 characters
excerpt: >
  **Offers** is a protocol for Lightning that
  allows nodes to request and receive invoices over LN.

## Optional.  Produces a Markdown link with either "[title][]" or
## "[title](link)"
primary_sources:
    - title: BOLT12

## Optional.  Each entry requires "title", "url", and "date".  May also use "feature:
## true" to bold entry
optech_mentions:
  - title: New proposed BOLT for offers protocol
    url: /en/newsletters/2019/11/13/#proposed-bolt-for-ln-offers

  - title: New direct messages protocol to be used for offers
    url: /en/newsletters/2020/02/26/#ln-direct-messages

  - title: "C-Lightning #4255 is the first of a series of PRs for offers"
    url: /en/newsletters/2020/12/16/#c-lightning-4255

  - title: "2020 year in review: LN offers"
    url: /en/newsletters/2020/12/23/#ln-offers

  - title: "C-Lightning 0.9.3 released with experimental offers support"
    url: /en/newsletters/2021/01/27/#c-lightning-0-9-3

  - title: Offers specification updated to partly address stuck payments
    url: /en/newsletters/2021/04/21/#using-ln-offers-to-partly-address-stuck-payments

  - title: "Offers specification updated to no longer require a signature"
    url: /en/newsletters/2021/07/14/#c-lightning-4625

  - title: C-Lightning 0.10.1 updates the experimental implementation of offers
    url: /en/newsletters/2021/08/11/#c-lightning-0-10-1

  - title: Spark Lightning Wallet adds partial support for offers
    url: /en/newsletters/2021/08/18/#spark-lightning-wallet-adds-bolt12-support

  - title: "Summary of LN developer conference, including discussion of offers"
    url: /en/newsletters/2021/11/10/#ln-summit-2021-notes

  - title: "2021 year-in-review: offers"
    url: /en/newsletters/2021/12/22/#offers

  - title: "Eclair #2117 adds onion message replies in preparation for supporting offers"
    url: /en/newsletters/2022/01/12/#eclair-2117

  - title: "Eclair #2416 adds support for receiving payments requested using the offers protocol"
    url: /en/newsletters/2022/09/21/#eclair-2416

  - title: "Core Lightning #5646 updates the implementation of offers to remove x-only public keys"
    url: /en/newsletters/2022/11/02/#core-lightning-5646

  - title: "Eclair #2499 allows specifying a blinded route to use when using a BOLT12 offer"
    url: /en/newsletters/2022/11/30/#eclair-2499

  - title: "LDK #1738 and #1908 provide additional features for handling offers"
    url: /en/newsletters/2023/01/04/#ldk-1738

  - title: "Core Lightning #5892 updates CLN’s implementation of the offers protocol"
    url: /en/newsletters/2023/02/08/#core-lightning-5892

  - title: "Eclair #2479 adds support for paying offers"
    url: /en/newsletters/2023/02/22/#eclair-2479

  - title: "LDK #1977 allows serializing and deserializing offers"
    url: /en/newsletters/2023/03/01/#ldk-1977

  - title: "LDK #2371 adds support for managing payments using offers"
    url: /en/newsletters/2023/09/20/#ldk-2371

  - title: "Ideas for creating a Lightning Address protocol compatible with offers"
    url: /en/newsletters/2023/11/22/#offers-compatible-ln-addresses

  - title: "Eclair #2752 allows an offer to reference a node using a short channel identifier (SCID)"
    url: /en/newsletters/2023/11/22/#eclair-2752

  - title: "Human readable payment instructions proposed that are compatible with offers"
    url: /en/newsletters/2024/02/21/#dns-based-human-readable-bitcoin-payment-instructions

  - title: "LDK #3078 adds support for inspection of BOLT12-returned invoices before payment"
    url: /en/newsletters/2024/06/21/#ldk-3078

  - title: "LDK #3082 adds an interface for building static reusable offers"
    url: /en/newsletters/2024/06/21/#ldk-3082

  - title: "Discussion of fully implementing offers versus incremently adding features from it"
    url: /en/newsletters/2024/07/05/#adding-a-bolt11-invoice-field-for-blinded-paths

  - title: "Core Lightning #7461 adds support for nodes to self-fetch and self-pay BOLT12 offers and invoices"
    url: /en/newsletters/2024/07/26/#core-lightning-7461

  - title: "CLN #7474 updates the offers plugin to understand the newly defined experimental TLV ranges"
    url: /en/newsletters/2024/08/02/#core-lightning-7474

  - title: "LDK #3139 improves the security of BOLT12 offers by authenticating the use of blinded paths"
    url: /en/newsletters/2024/08/02/#ldk-3139

  - title: "Proposal to allow opt-in identification and authentication of LN payers when using offers"
    url: /en/newsletters/2024/08/16/#optional-identification-and-authentication-of-ln-payers

  - title: "LDK #3140 adds support for paying static BOLT12 invoices to send async payments"
    url: /en/newsletters/2024/09/20/#ldk-3140

  - title: "BOLTs #798 merges the offers protocol specification which introduces BOLT12"
    url: /en/newsletters/2024/10/04/#bolts-798

  - title: "Core Lightning #7833 enables the offers protocol by default"
    url: /en/newsletters/2024/11/22/#core-lightning-7833

  - title: "LDK #3446 adds support for including a trampoline payment flag in a BOLT12 invoice"
    url: /en/newsletters/2024/12/13/#ldk-3446

  - title: "BOLT12 update to allow optional inclusion of BIP353 human-readable Bitcoin payment instructions"
    url: /en/newsletters/2024/12/13/#bolts-1180

  - title: "LDK #3649 adds support for paying Lightning Service Providers (LSPs) with BOLT12 offers"
    url: /en/newsletters/2025/03/28/#ldk-3649

## Optional.  Same format as "primary_sources" above
see_also:
  - title: Blinded paths
    link: topic rv routing
---
An example of a common use of this protocol would be that a merchant
generates a QR code, the customer scans the QR code, the customer’s LN
node sends some of the details from the QR code (such as an order ID
number) to the merchant’s node over LN, the merchant’s node returns an
invoice (also over LN), the invoice is displayed to the user (who
agrees to pay), and the payment is sent.

Although the above use case was previously addressed using
[BOLT11][] invoices, the ability for the spending and receiving nodes
to communicate directly before attempting payment provides much more
flexibility. For example, the requested amount could be specified in
the terms of a non-Bitcoin currency (e.g. USD); if the BTC-to-USD
exchange rate changed too much since the invoice was received, the two
nodes could automatically negotiate an update to the payable BTC
amount to make it again consistent with the requested USD amount.

Interactive communication between the nodes also enables features that
aren’t possible with BOLT11’s one-time-use hashlocks, such as
recurring payments for subscriptions and donations.

{% include references.md %}
