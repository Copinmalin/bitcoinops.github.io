---
title: Uneconomical outputs

## Optional.  Shorter name to use for reference style links e.g., "foo"
## will allow using the link [topic foo][].  Not case sensitive
# shortname: foo

## Optional.  An entry will be added to the topics index for each alias
title-aliases:
  - Dust

## Required.  At least one category to which this topic belongs.  See
## schema for options
topic-categories:
  - Transaction Relay Policy
  - Privacy Problems

## Optional.  Produces a Markdown link with either "[title][]" or
## "[title](link)"
primary_sources:
    - title: Bitcoin Core dust limit code comment
      link: https://github.com/bitcoin/bitcoin/blob/439e58c4d8194ca37f70346727d31f52e69592ec/src/policy/policy.cpp#L14

## Optional.  Each entry requires "title", "url", and "date".  May also use "feature:
## true" to bold entry
optech_mentions:
  - title: "Question: how does LN handle dust and uneconomical payments?"
    url: /en/newsletters/2019/04/30/#do-htlcs-work-for-micropayments

  - title: "Question: how was the dust limit chosen?"
    url: /en/newsletters/2019/04/30/#how-was-the-dust-limit-of-546-satoshis-was-chosen-why-not-550-satoshis

  - title: "LND #3809 adds a force parameter to the BumpFee RPC so that it can spend uneconomical UTXOs"
    url: /en/newsletters/2020/01/29/#lnd-3809

  - title: "Discussion about removing the dust limit"
    url: /en/newsletters/2021/08/18/#dust-limit-discussion

  - title: "Rust-Lightning #1009 adds a `max_dust_htlc_exposure_msat` channel configuration option"
    url: /en/newsletters/2021/08/18/#rust-lightning-1009

  - title: "Multiple implementations of BOLTs #894 which allow using a lower commitment tx dust limit"
    url: /en/newsletters/2021/10/06/#eclair-1900

  - title: "Multiple implementations of LN vulnerable to uneconomical spending CVEs"
    url: /en/newsletters/2021/10/13/#ln-spend-to-fees-cve

  - title: "Bitcoin Core #22863 documents P2TR dust amount"
    url: /en/newsletters/2021/10/20/#bitcoin-core-22863

  - title: "BOLTs #894 specifies various checks related to uneconomical payments in LN"
    url: /en/newsletters/2021/10/20/#bolts-894

  - title: "Discussion about removing the dust limit for one particular case"
    url: /en/newsletters/2021/12/15/#adding-a-special-exception-for-certain-uneconomical-outputs

  - title: "Question about problems removing uneconomical outputs from UTXO set"
    url: /en/newsletters/2022/07/27/#does-an-uneconomical-output-need-to-be-kept-in-the-utxo-set

  - title: "BDK #689 allows a wallet to create a transaction that violates the dust limit"
    url: /en/newsletters/2022/09/07/#bdk-689

  - title: "Discussion about allowing uneconomical outputs that are part of a transaction package"
    url: /en/newsletters/2022/10/05/#ephemeral-dust

  - title: "BOLTs #919 suggests LN nodes limit their maximum exposure to uneconomical HTLCs"
    url: /en/newsletters/2023/08/23/#bolts-919

  - title: "LDK #3268 adds a more conservative fee estimation method for dust calculations"
    url: /en/newsletters/2024/09/06/#ldk-3268

  - title: "Bitcoin Core PR Review Club about exempting ephemeral anchors from the dust limit"
    url: /en/newsletters/2024/11/08/#bitcoin-core-pr-review-club

  - title: "Proposal for removing uneconomical outputs from the stored UTXO set"
    url: /en/newsletters/2025/06/06/#removing-outputs-from-the-utxo-set-based-on-value-and-time

## Optional.  Same format as "primary_sources" above
see_also:
  - title: Dust attacks (output linking)
    link: topic output linking

  - title: Ephemeral anchors
    link: topic ephemeral anchors

## Optional.  Force the display (true) or non-display (false) of stub
## topic notice.  Default is to display if the page.content is below a
## threshold word count
#stub: false

## Required.  Use Markdown formatting.  Only one paragraph.  No links allowed.
## Should be less than 500 characters
excerpt: >
  **Uneconomical outputs** are transaction outputs that are worth less
  than the fees it will cost to spend them.  To prevent users from
  creating uneconomical outputs that will increase the size of the UTXO
  set,  Bitcoin Core and other nodes refuse to relay or mine
  transactions with outputs below a certain value, called the **dust
  limit**.

---
**Terminology note:** sometimes *dust* is used as a synonym for
*uneconomical outputs* or, more generically, *low value outputs*.  This
can create confusion, such as in the case of [dust attacks][] which
involve amounts just barely above the dust limit.  Optech
[recommends][optech style] using *uneconomical outputs* for outputs that
aren't worth the cost to spend them, reserving the term *dust* for
references specific to the dust limit.

[dust attacks]: /en/topics/output-linking/
[optech style]: https://github.com/bitcoinops/bitcoinops.github.io/blob/master/STYLE.md

{% include references.md %}
{% include linkers/issues.md issues="" %}
