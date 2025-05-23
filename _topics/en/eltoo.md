---
title: Eltoo

title-aliases:
  - LN-Symmetry

## Required.  At least one category to which this topic belongs.  See
## schema for options
topic-categories:
  - Lightning Network
  - Contract Protocols

## Required.  Use Markdown formatting.  Only one paragraph.  No links allowed.
excerpt: >
  **Eltoo** (also called **LN-Symmetry**) is a proposed enforcement mechanism for LN that allows any later
  channel state to replace any earlier channel state.  Although eltoo
  can be used with a penalty mechanism similar to the one used with
  existing LN channels, eltoo doesn't need the penalty mechanism in
  order to be secure.

## Optional.  Produces a Markdown link with either "[title][]" or
## "[title](link)"
primary_sources:
    - title: Eltoo
      link: https://blockstream.com/eltoo.pdf

    - title: LN-Symmetry Project
      link: https://delvingbitcoin.org/t/ln-symmetry-project-recap/359

## Optional.  Each entry requires "title", "url", and "date".  May also use "feature:
## true" to bold entry
optech_mentions:
  - title: "2018 year-in-review: Eltoo"
    url: /en/newsletters/2018/12/28#april

  - title: Optimization for Eltoo-based payment channels
    url: /en/newsletters/2019/01/08/#continued-sighash-discussion

  - title: SIGHASH_ANYPREVOUT proposal compatible with Eltoo
    url: /en/newsletters/2019/05/21/#proposed-anyprevout-sighash-modes

  - title: Eltoo demo implementation
    url: /en/newsletters/2019/09/11/#eltoo-sample-implementation-and-discussion

  - title: "Modification to `SIGHASH_ANYPREVOUTANYSCRIPT` to improve eltoo flexibility"
    url: /en/newsletters/2020/01/29/#layered-commitments-with-eltoo

  - title: Implementing statechains without eltoo
    url: /en/newsletters/2020/04/01/#implementing-statechains-without-schnorr-or-eltoo

  - title: "Impact of SIGHASH_NOINPUT and eltoo on LN backups"
    url: /en/newsletters/2020/06/03/#ln-backups

  - title: Upgrading LN commitment formats, including for eltoo
    url: /en/newsletters/2020/07/29/#upgrading-channel-commitment-formats

  - title: Using attacks like transaction pinning and selective relay against eltoo
    url: /en/newsletters/2020/08/12/#discussion-about-eltoo-and-sighash-anyprevout

  - title: Eltoo demo implementation with new blog post overview
    url: /en/newsletters/2021/09/01/#eltoo-example-channel

  - title: "Inherited identifiers proposal with an alternative channel commiment mechanism to eltoo"
    url: /en/newsletters/2021/10/06/#proposal-for-transaction-heritage-identifiers

  - title: "LN PTLC proposal providing some of the same benefits of eltoo without a soft fork"
    url: /en/newsletters/2021/10/13/#multiple-proposed-ln-improvements

  - title: "Summary of LN developer conference, including discussion of eltoo"
    url: /en/newsletters/2021/11/10/#ln-summit-2021-notes

  - title: "Using transaction introspection to prevent pinning in eltoo channels"
    url: /en/newsletters/2022/05/18/#using-transaction-introspection-to-prevent-rbf-pinning

  - title: "Discussion about the use of the annex field in LN-symmetry"
    url: /en/newsletters/2023/06/14/#discussion-about-the-taproot-annex

  - title: "Using eltoo-compatible covenants to improve LN scalability"
    url: /en/newsletters/2023/09/27/#using-covenants-to-improve-ln-scalability

  - title: "LN-Symmetry research implementation with summary of initial results"
    url: /en/newsletters/2024/01/10/#ln-symmetry-research-implementation

  - title: "Post and website examining LN-Symmetry testing on the default signet"
    url: /en/newsletters/2024/11/22/#signet-activity-report

  - title: "Discussion about contract-level relative timelocks to solve LN-Symmetry's 2x delay problem"
    url: /en/newsletters/2025/01/10/#contract-level-relative-timelocks

  - title: "Multiparty LN-Symmetry variant with penalties for limiting published updates"
    url: /en/newsletters/2025/01/10/#multiparty-ln-symmetry-variant-with-penalties-for-limiting-published-updates

  - title: "Summary and criticism of CTV + CSFS benefits for LN-Symmetry"
    url: /en/newsletters/2025/04/04/#ln-symmetry

## Optional.  Same format as "primary_sources" above
see_also:
  - title: SIGHASH_ANYPREVOUT
    link: topic sighash_anyprevout
---
If eltoo is used without a penalty mechanism, there's no harm in
publishing an old state, except that it costs transaction fees to
publish.  This makes it less dangerous to try to restore an LN node
from a backup after a sudden failure or some other problem.  It also
makes it much simpler for three or more parties to open a single LN
channel together, enabling features such as [channel factories][topic
channel factories].

Another consequence of LN channels without penalties is that LN nodes
using eltoo only need to store the latest state.  For certain devices
that lack large amounts of persistent storage (for example, hardware
wallets), they may not be able to store enough data to effectively use
penalty-based LN---but as long as they can store a few kB, they should
be able to use eltoo-based LN.

{% include references.md %}
