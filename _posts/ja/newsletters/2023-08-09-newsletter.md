---
title: 'Bitcoin Optech Newsletter #263'
permalink: /ja/newsletters/2023/08/09/
name: 2023-08-09-newsletter-ja
slug: 2023-08-09-newsletter-ja
type: newsletter
layout: newsletter
lang: ja
---
今週のニュースレターは、LibbitcoinのBitcoin Explorer（bx）ツールの使用における深刻な脆弱性について警告し、
サービス拒否（DoS）防御の設計に関する議論と、HTLCエンドースメントに関するテストとデータ収集の計画の発表、
Bitcoin Coreのトランザクションリレーポリシーに対する2つの変更案を掲載しています。
また、Bitcoin Core PR Review Clubミーティングの要約や、新しいリリースとリリース候補の発表、
人気のあるBitcoinインフラストラクチャソフトウェアの注目すべき変更など、恒例のセクションも含まれています。

## 要処置事項

- **<!--severe-libbitcoin-bitcoin-explorer-vulnerability-->深刻なLibbitcoin Bitcoin Explorerの脆弱性:**
  `bx seed`コマンドを使用して[BIP32][topic BIP32]シードや、[BIP39][]ニーモニック、
  秘密鍵、またはその他の秘密情報を作成した場合は、資金を別の安全なアドレスに直ちに移動することを検討してください。
  詳細については、以下のニュースセクションを参照してください。

## ニュース

- **サービス拒否（DoS）防御の設計哲学:** Anthony Townsは、
  先日のLN開発者ミーティング（[ニュースレター #261][news261 jamming]参照）の議事録の
  [チャネルジャミング][topic channel jamming attacks]に関する部分に対して、
  Lightning-Devメーリングリストに[投稿][towns dos]しました。
  議事録には、「攻撃者を抑止するコストは、誠実なユーザーにとっては不合理で、
  誠実なユーザーにとって妥当なコストは、攻撃者を抑止するには低すぎる」と書かれていました。

  Townsは、攻撃者を高いコストで排除する代わりに、攻撃者と誠実なユーザーの双方が支払うコストに、
  サービスを提供するノードオペレーターが支払う根本的なコストを反映させることを提案しました。
  そうすることで、誠実なユーザーにサービスを提供することで相応の利益を得ているノードオペレーターは、
  攻撃者がそのサービスを利用し始めたとしても、相応の利益を得続けることができます。
  攻撃者がノードのリソースを過剰に消費して誠実なユーザーへのサービスを拒否しようとした場合、
  それらのリソースを提供するノードには、提供するリソースをスケールアップするインセンティブ、
  つまりより大きな収入が得られます。

  このスキームがどのように機能するかの提案として、Townsは、
  支払いが成功した場合の通常の手数料に加えて請求される転送コミットメント手数料とリバースホールド手数料の組み合わせに関する
  数年前のアイディア（[ニュースレター #86][news86 hold fees]参照）を復活させました。
  HTLCが支払人のアリスから転送ノードのボブに伝播すると、
  アリスは少額の転送コミットメント手数料を支払います。その手数料の内、ボブの部分は、
  HTLCの処理コスト（帯域幅など）に相当します。ボブはHTLCを受け入れた後、
  HTLCが決済されるまでの間、アリスに対して定期的に少額のリバースホールド手数料を支払う責任があります。
  これにより、支払いの受諾または支払いのキャンセルによる遅延が補償されます。
  ボブが支払いを受け取った後すぐにキャロルに転送した場合、
  ボブはアリスから受け取ったよりもわずかに少ない転送コミットメント手数料をキャロルに支払い（この差額が実際の報酬として受け取る金額になります）、
  キャロルはボブにわずかに大きいリバースホールド手数料を提供します（繰り返しますが、この差額がボブの報酬です）。
  転送ノードや受信者がHTLCを遅延させない限り、通常の成功の手数料にかかる追加コストは少額の転送コミットメント手数料のみです。
  ただし、受信者またはいずれかのホップが支払いを遅延した場合、
  最終的には上流ノードのすべてのリバースホールド手数料を支払う責任を負うことになります。

  Clara Shikhelmanは、一定期間にわたって支払われるリバースホールド手数料は、
  同じ期間、同じ量の資本に対してノードが成功手数料から得る金額を簡単に超える可能性があると[返信しました][shikhelman dos]。
  そのため、悪意あるノードがメカニズムを悪用して相手から手数料を徴収することが誘発される可能性があります。
  彼女は、Townsが描いたようなメカニズムが直面するであろういくつかの課題について説明し、
  Townsは[返信][towns dos2]で反論し、次のようにまとめています「
  たとえ現在の実装作業がレピュテーションベースの方法に焦点を当てているとしても、
  人々が興味を持っていれば、金銭ベースのDoSの抑止は依然として有益な研究分野になる可能性が高いと思います」。

- **HTLCエンドースメントのテストとデータ収集:** Carla Kirk-CohenとClara Shikhelmanは、
  EclairとCore LightningおよびLNDに関連する開発者が、データ収集を開始するために
  [HTLCエンドースメント][topic htlc endorsement]プロトコルの一部を実装していることを
  Lightning-Devメーリングリストに[投稿しました][kcs endorsement]。
  これを支援するために、研究者のためにテストノードが収集するのに役立つデータのセットを提案しています。
  これらのフィールドの多くは、支払人と受信者のプライバシーを損なう可能性のある情報の漏洩を防ぐために、
  データをランダム化することを意図しています。テストには複数のフェーズがあり、
  参加ノードがそれぞれのフェーズでどのように動作するかを概説しています。

- **Bitcoin Coreのデフォルトリレーポリシーの変更の提案:** Peter Toddは、
  Bitcoin Coreのデフォルトのリレーポリシーを変更するために公開されたプルリクエストに関連する2つのスレッドを
  Bitcoin-Devメーリングリスト上で開始しました。

  - *デフォルトでフルRBF:* [最初のスレッド][todd rbf]と[プルリクエスト][bitcoin core #28132]は、
    Bitcoin Coreの将来のバージョンで[フルRBF][topic rbf]をデフォルト設定にすることを提案しています。
    現在Bitcoin Coreは、デフォルトでは、_オプトインRBF_ と呼ばれる置換されるトランザクションにオプトインの置換可能性を示す[BIP125][]シグナルが含まれている場合
    （そして、元のトランザクションと置換トランザクションの両方が他のルールに準拠している場合）のみ、
    未承認トランザクションの置換をmempoolに受け入れ、リレーします。
    `-mempoolfullrbf`という設定オプションを使用すると、ノードオペレーターは、
    BIP125シグナルが含まれていない場合でも、未承認トランザクションの置換を受け入れることができます。
    これは _フルRBF_ と呼ばれます（[ニュースレター #208][news208 rbf]参照）。
    Peter Toddの提案は、フルRBFをデフォルトにする一方で、
    ノードオペレーターがオプトインRBFを選択するように設定を変更できるようにするものです。

    Peter Toddは、（[疑問視されている][towns rbf]彼の計測によると）
    マイニングのハッシュレートのかなりの割合がフルRBFルールに従っており、
    フルRBFを有効にし、シグナルのない置換がこれらのマイナーに到達できるようにするためのリレーノードが十分あるため、
    この変更は正当であると主張しています。彼はまた、
    現在未承認のオンチェーントランザクションを最終的な支払いとして受け入れている活動的な企業を知らないとも述べています。

  - *`OP_RETURN`アウトプットに対する特定の制限の削除:* [2つめのスレッド][todd opr]と[プルリクエスト][bitcoin core #28130]は、
    `OP_RETURN` opcodeで始まるアウトプット（_OP_RETURNアウトプット_）を持つトランザクションに対する
    Bitcoin Coreの特定の制限を削除することを提案しています。現在、Bitcoin Coreは、
    （デフォルトでは）複数の`OP_RETURN`アウトプットや、
    サイズが83バイト（80バイトの任意ののデータに相当）を超えるアウトプットスクリプトを持つ`OP_RETURN`アウトプットを持つ
    トランザクションをリレーしたり、mempoolに受け入れたりしません。

    少量のデータを持つ`OP_RETURN`アウトプットのリレーとデフォルトでマイニングを許可することは、
    UTXOセットに（多くの場合、永続的に）保存する必要がある他のタイプのアウトプットにデータを保存していたのがきっかけでした。
    `OP_RETURN`アウトプットは、UTXOセットに保存する必要がないため、
    それほど問題はありません。その後、一部の人々が大量のデータをトランザクションのwitnessに保存し始めました。

    プルリクエストは、トランザクションがBitcoin Coreの他のリレーポリシーに従っている場合に限り
    （たとえば、トランザクションの合計サイズが100,000 vbyte未満など）、デフォルトで任意の数の`OP_RETURN`アウトプットと、
    任意の量のデータを含む`OP_RETURN`アウトプットを許可するようにします。
    この記事の執筆時点では、プルリクエストに対する意見はさまざまで、
    緩和されたポリシーによりブロックチェーンに保存される非金融データの量が増加すると主張する開発者もいれば、
    ブロックチェーンにデータを追加する他の方法が使用されている時に、
    `OP_RETURN`アウトプットの使用を妨げる理由はないと主張する開発者もいます。

- **Libbitcoin Bitcoin Explorerのセキュリティの開示**
  Libbitcoinのユーザー間で最近発生したビットコインの紛失事件を調査していた複数のセキュリティ研究者は、
  プログラムのBitcoin Explorer (bx)ツールの`seed`コマンドが、約40億個の異なるユニークな値しか生成しないことを[発見][milksad]しました。
  その値が、秘密鍵や特定の導出パス（たとえば、BIP39に従う）を持つウォレットを作成するために使用されているだろうと仮定する攻撃者は、
  単一の一般的なコンピューターを使用して1日以内にすべての可能なウォレットを検索し、
  その鍵やウォレットで受信したすべての資金を盗むことができる可能性があります。
  このような盗難は2023年7月12日に発生したと思われるものがあり、約30BTC（当時約85万ドル）の損失が発生しました。

  資金の喪失につながったと思われるプロセスと同様のプロセスが、書籍
  _Mastering Bitcoin_ や、Bitcoin Explorerの[ホームページのドキュメント][bx home]、
  Bitcoin Explorerの他の多くの場所のドキュメント（例：[1][bx1]、[2][bx2]、[3][bx3]）に[掲載されている][mb milksad]ことが判明しています。
  `seed`コマンドの[オンラインドキュメント][seed doc]を除いて、
  どのドキュメントも明確に安全でないことを警告していませんでした。

  Optechの推奨事項は、ウォレットやアドレスを生成するのに`bx seed`を使用した可能性がある人は、
  [開示ページ][milksad]を確認し、脆弱なシードをテストするために彼らが提供するサービスを使用することです。
  攻撃者が発見したのと同じプロセスを使用した場合、あなたのビットコインはすでに盗まれている可能性が高いですが、
  プロセスの別のバリエーションを使用した場合は、ビットコインを安全な場所に移動するチャンスがまだあるかもしれません。

  [CVE-2023-39910][]の[責任ある開示][topic responsible disclosures]に多大な労力を払ってくれた研究者に感謝します。

## Bitcoin Core PR Review Club

*この毎月のセクションでは、最近の[Bitcoin Core PR Review Club][]ミーティングを要約し、
重要な質問と回答のいくつかに焦点を当てます。
以下の質問をクリックしてミーティングでの回答の要約を確認してください。*

[Silent Payments: Implement BIP352][review club 28122]は、josibakeによるPRで、
Bitcoin Coreのウォレットに[サイレントペイメント][topic silent payments]を追加する最初のステップです。
このPRは、[BIP352][]のロジックのみを実装し、ウォレットの変更は含まれていません。

{% include functions/details-list.md
  q0="なぜPRでは、`secp256k1`が提供するデフォルトのハッシュ関数を使用するのではなく、カスタムのECDHハッシュ関数を追加してるのですか？"
  a0="実際にはECDHの結果をハッシュする必要はありません。
      カスタム関数は、ECDH操作の結果に対する`sha256`がデフォルトで適用されるのを防ぎます。
      これは、トランザクションの作成者がすべてのインプットを管理していない場合に必要です。
      ECDH中に結果をハッシュしないことで、個々の参加者は自分の秘密鍵だけでECDHを行い、部分的なECDHを渡すことができます。
      その後、部分的なECDHの結果を合算し、残りのプロトコル実行します（カウンターによるハッシュなど）。"
  a0link="https://bitcoincore.reviews/28122#l-126"

  q1="PRは、サイレントペイメントアドレスのエンコードとデコード用の関数を追加しています。
      既存のエンコーダークラスとデコーダー関数を使用して、新しい種類の`CTxDestination`として追加できないのは何故ですか？"
  a1="サイレントペイメントアドレスは、実際には特定のアウトプットスクリプトをエンコードしません。
      `scriptPubKey`ではありません。むしろ、実際のアウトプットスクリプトを導出するために必要な公開鍵をエンコードし、
      また、サイレントペイメントトランザクションのインプットに依存します。
      つまり、（従来のアドレスのように）送信先の`scriptPubKey`を提供するのではなく、
      サイレントペイメントアドレスは、ECDHを実行するための公開鍵を提供し、
      その共有シークレットを、受信者が検出し後で使用できるようになる`scriptPubKey`に変換する方法をプロトコルが指示します。"
  a1link="https://bitcoincore.reviews/28122#l-153"

  q2="[BIP352][]は、バージョン管理と前方互換性について言及しています。
      前方互換性とは何で、なぜ重要なのですか？"
  a2="これは、たとえばv0ウォレットが、v1（およびv2など）のサイレントペイメントアドレスをデコードして送信することを可能にします
      （たとえ、ウォレットがv1アドレスを生成できなくても）。
      これは、新しいバージョンが作成された時に、ウォレットがすぐにアップグレードする必要がない
      （またはすべての機能を失うことがない）ようにするために重要です。"
  a2link="https://bitcoincore.reviews/28122#l-170"

  q3="新しいバージョンが意図的に互換性を破壊したい場合は？"
  a3="v31が互換性を破壊するようなアップグレードのために予約されています。"
  a3link="https://bitcoincore.reviews/28122#l-186"

  q4="互換性を破壊するバージョン番号（v31）を1つだけ割り当てても問題ないのは何故ですか？"
  a4="必要に応じて、破壊バージョン以降のバージョンをどのように扱うかについての新しいルールの定義を延期することができます。"
  a4link="https://bitcoincore.reviews/28122#l-188"

  q5="`DecodeSilentAddress`では、バージョンとデータサイズのチェックがあります。
      このチェックは何をしていて、なぜ重要なのですか？"
  a5="新しいバージョンでさらにデータが追加される場合、前方互換性のある部分のみを取得する方法が必要です。
      これは、最初の66バイト（v0フォーマット）のみを解析する必要があることを意味します。
      これは前方互換性のために重要です。"
  a5link="https://bitcoincore.reviews/28122#l-194"

  q6="新しいサイレントペイメントのコードは、ウォレットディレクトリの`src/wallet/silentpayments.cpp`にあります。
      ここは適切な場所ですか？ウォレットのコンテキストの外でサイレントペイメントのコードを使用したいユースケースを思いつきますか？"
  a6="軽量なサイレントペイメントウォレットの代わりに、サイレントペイメントを検出する（または関連する計算を行う）
      ウォレットのないサーバーを実装したい場合には理想的ではありません。
      フルノードがトランザクションのために調整データをインデックス化し、
      軽量クライアントがそれを照会できるように保存したり、
      [BIP158][]のようなフィルターを介してそのデータを提供したりするユースケースが想像できます。
      ただ、そのようなユースケースが現れるまでは、`src/wallet`に置いておく方がコードの整理に役立ちます。"
  a6link="https://bitcoincore.reviews/28122#l-205"

  q7="PRで、`Recipient`クラスは2つの秘密鍵（spendとscan）を使用して初期化されます。
      スキャンには両方の鍵が必要ですか？"
  a7="いいえ、必要なのはscan keyのみです。
      spend keyなしでサイレントペイメントをスキャンする機能は、将来実装される可能性があります。"
  a7link="https://bitcoincore.reviews/28122#l-217"
%}

## リリースとリリース候補

*人気のBitcoinインフラストラクチャプロジェクトの新しいリリースとリリース候補。
新しいリリースにアップグレードしたり、リリース候補のテストを支援することを検討してください。*

- [BDK 0.28.1][]は、ウォレットアプリケーションを構築するためのこの人気のライブラリのリリースです。
  このリリースには、バグ修正と[ディスクリプター][topic descriptors]で[P2TR][topic taproot]の
  [BIP86][]導出パスを使用するためのテンプレートの追加が含まれています。

## 注目すべきコードとドキュメントの変更

*今週の[Bitcoin Core][bitcoin core repo]、[Core
Lightning][core lightning repo]、[Eclair][eclair repo]、[LDK][ldk repo]、
[LND][lnd repo]、[libsecp256k1][libsecp256k1 repo]、[Hardware Wallet
Interface (HWI)][hwi repo]、[Rust Bitcoin][rust bitcoin repo]、[BTCPay
Server][btcpay server repo]、[BDK][bdk repo]、[Bitcoin Improvement
Proposals（BIP）][bips repo]、[Lightning BOLTs][bolts repo]および
[Bitcoin Inquisition][bitcoin inquisition repo]の注目すべき変更点。*

- [Bitcoin Core #27746][]は、ブロックをディスクに保存するかどうかの決定を
  chainstateに依存しない検証ロジックに移動することで、
  ブロックストレージとchainstateオブジェクトの関係を簡素化します。
  ブロックをディスクに保存するかどうかの決定は、UTXOの状態を必要としない検証ルールに関連しています。
  以前、Bitcoin CoreはDoS対策の理由からchainstate固有のヒューリスティックを使用していましたが、
  [assumeUTXO][topic assumeutxo]と2つのchainstateが共存する可能性を考慮して、
  提案された分離を達成するために再構築されました。

- [Core Lightning #6376][]と[#6475][core lightning #6475]は、
  Pickhardt Paymentを使用して最適なマルチパスペイメント（[ニュースレター #192][news192 pp]参照）を構築する`renepay`と呼ばれるプラグインを実装しました。
  Pickhardt Paymentは、各チャネルの流動性がフローの方向に0から最大キャパシティまでランダムに分布すると仮定しています。
  支払額が大きいと、経路に沿って十分な流動性が適用されない可能性があるため、失敗する可能性があります。
  一方、支払いを多数のパーツに分割すると、それぞれの個別の経路で失敗する可能性があるため、失敗する可能性があります。
  支払いは次に、支払いのパーツの数とパーツ毎の金額の中間点を見つけることを目的として、
  ライトニングネットワーク内のフローとしてモデル化されます。
  このアプローチを使用することで、Pickhardt Paymentは、成功の可能性を最大化しながら、
  キャパシティと残高の制約を満たす最適なフローを見つけます。不完全な支払いの試行の応答は、
  関係するすべてのチャネルの想定される流動性分布を更新するために使用され、
  転送に失敗したチャネルを減らすだけでなく、成功した金額も考慮します。
  フロー計算にベース手数料を組み込むことは計算的に困難であるため（[ニュースレター #163][news163 base]参照）、
  支払いの計画に`renepay`を使用するノードは、代わりにベース手数料がゼロでないチャネルの相対手数料を過大評価します。
  支払いを配信するために構築されたOnionパッケージでは、実際の手数料が使用されます。

- [Core Lightning #6466][]と[#6473][core lightning #6473]は、
  [BIP93][]で定義されている[codex32][topic codex32]形式で
  ウォレットの[マスターシークレット][topic BIP32]をバックアップ・復元するサポートを追加しました。

- [Core Lightning #6253][]と[#5675][core lightning #5675]は、
  [スプライシング][topic splicing]のドラフト仕様[BOLTs #863][]の実験的な実装を追加しました。
  チャネルの双方がスプライシングをサポートしている場合、
  オンチェーントランザクションを使用してチャネルに資金をスプライス・インしたり、
  オンチェーンで使用することでチャネルから資金をスプライス・アウトしたりできます。
  どちらの操作もチャネルを閉じる必要はなく、
  オンチェーンのスプライシングトランザクションが安全な深さで承認されるのを待ちながら、
  元の残高で残っている金額を使用して支払いの送信、受信、または転送を続けることができます。
  安全な深さになると、その時点でチャネルにスプライス・インした資金も利用できるようになります。
  スプライシングの主な利点は、LN対応ウォレットが資金の大部分をオフチェーンで保持し、
  要求に応じてその残高からオンチェーン支払いを作成できることです。これにより、
  ウォレットはユーザーにオフチェーンとオンチェーンの資金を分けて表示するのではなく、
  単一の残高を表示できるようになります。

- [Rust Bitcoin #1945][]は、PRが単なるリファクタリングである場合、
  マージされる前にどの程度のレビューが必要かというプロジェクトのポリシーを変更しました。
  リファクタリングや小さな変更を他のPRと同じ高い基準でレビューすることに課題を抱えている他のプロジェクトは、
  Rust Bitcoinの新しいポリシーを調査するといいでしょう。

- [BOLTs #759][]は、LNの仕様に[Onionメッセージ][topic onion messages]のサポートを追加しました。
  Onionメッセージは、ネットワーク上で一方向のメッセージの送信を可能にします。
  支払い（HTLC）と同様に、メッセージはOnion暗号化され、各転送ノードは、
  どのピアからメッセージを受信したかと、次にメッセージを受信するピアのみを認識します。
  メッセージペイロードも暗号化されるため、最終的な受信者のみがそれを読むことができます。
  （コミットメントが受信者に向かって下流に流れ、支払いの請求に必要なプリイメージは送信者に向かって上流に流れる）
  双方向のHTLCの転送とは異なり、Onionメッセージの一方向性は、
  転送ノードがメッセージの転送後に何も保存する必要がないことを意味します。
  ただし、提案されているいくつかのサービス拒否保護の仕組みの中には、
  ピア毎に少量の集約情報を保持することに依存しているものがあります（[ニュースレター #207][news207 onion]参照）。
  双方向のメッセージングは、元の送信者がメッセージに戻りのパスを含めることで実現できます。
  Onionメッセージは、数ヶ月前にLNの仕様に追加された
  [ブラインド・パス][topic rv routing]（[ニュースレター #245][news245 blinded]参照）を使用し、
  Onionメッセージ自体は、開発中の[Offerプロトコル][topic offers]で使用されています。

{% include references.md %}
{% include linkers/issues.md v=2 issues="27746,6376,6475,6466,6473,6253,5675,863,1945,759,28132,28130" %}
[news245 blinded]: /ja/newsletters/2023/04/05/#bolts-765
[towns dos]: https://gnusha.org/url/https://lists.linuxfoundation.org/pipermail/lightning-dev/2023-July/004020.html
[news86 hold fees]: /ja/newsletters/2020/02/26/#reverse-up-front-payments
[shikhelman dos]: https://gnusha.org/url/https://lists.linuxfoundation.org/pipermail/lightning-dev/2023-July/004033.html
[towns dos2]: https://gnusha.org/url/https://lists.linuxfoundation.org/pipermail/lightning-dev/2023-August/004035.html
[kcs endorsement]: https://gnusha.org/url/https://lists.linuxfoundation.org/pipermail/lightning-dev/2023-August/004034.html
[todd rbf]: https://gnusha.org/url/https://lists.linuxfoundation.org/pipermail/bitcoin-dev/2023-July/021823.html
[towns rbf]: https://github.com/bitcoin/bitcoin/pull/28132#issuecomment-1657669845
[news207 onion]: /ja/newsletters/2022/07/06/#onion-message-rate-limiting
[news261 jamming]: /ja/newsletters/2023/07/26/#channel-jamming-mitigation-proposals
[todd opr]: https://gnusha.org/url/https://lists.linuxfoundation.org/pipermail/bitcoin-dev/2023-August/021840.html
[CVE-2023-39910]: https://cve.mitre.org/cgi-bin/cvename.cgi?name=CVE-2023-39910
[milksad]: https://milksad.info/
[mb milksad]: https://github.com/bitcoinbook/bitcoinbook/commit/76c5ba8000d6de20b4adaf802329b501a5d5d1db#diff-7a291d80bf434822f6a737f3e564be6a67432e2f3f12669cf0469aedf56849bbR126-R134
[bx home]: https://web.archive.org/web/20230319035342/https://github.com/libbitcoin/libbitcoin-explorer/wiki
[bx1]: https://web.archive.org/web/20210122102649/https://github.com/libbitcoin/libbitcoin-explorer/wiki/How-to-Receive-Bitcoin
[bx2]: https://web.archive.org/web/20210122102714/https://github.com/libbitcoin/libbitcoin-explorer/wiki/bx-mnemonic-new
[bx3]: https://web.archive.org/web/20210506162634/https://github.com/libbitcoin/libbitcoin-explorer/wiki/bx-hd-new
[seed doc]: https://web.archive.org/web/20210122102710/https://github.com/libbitcoin/libbitcoin-explorer/wiki/bx-seed
[news208 rbf]: /ja/newsletters/2022/07/13/#bitcoin-core-25353
[bdk 0.28.1]: https://github.com/bitcoindevkit/bdk/releases/tag/v0.28.1
[review club 28122]: https://bitcoincore.reviews/28122
[bip352]: https://github.com/bitcoin/bips/pull/1458
[bip158]: https://github.com/bitcoin/bips/blob/master/bip-0158.mediawiki
[news192 pp]: /ja/newsletters/2022/03/23/#payment-delivery-algorithm-update
[news163 base]: /ja/newsletters/2021/08/25/#zero-base-fee-ln-discussion-ln