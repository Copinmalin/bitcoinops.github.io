{:.post-meta}
*作者：[Philip Glazman][]，[River Financial][] 工程师*

*River Financial 是一家专注于比特币金融服务的新兴金融机构。其旗舰产品——比特币经纪业务，为零售投资者提供了一个高接触的平台，方便他们买卖比特币。*

River Financial 在其钱包软件中使用了两项技术：[部分签名的比特币交易（PSBT）][topic psbt] 和[输出脚本描述符][topic descriptors]。采用这些标准的决定使得 River 的钱包操作具有更大的灵活性和互操作性。

将 PSBT 引入钱包栈的决定受到了将密钥签名者视为接口这一理念的影响。PSBT 是由 Andrew Chow 编写的 [BIP174][] 中描述的签名者格式。在此标准之前，没有标准化格式来描述未签名交易。因此，每个签名者都使用特定于供应商的格式，这些格式无法互操作。通过遵循 PSBT 标准，钱包基础设施可以避免供应商锁定，减少签名者逻辑中的攻击面，并对钱包创建的交易有更好的保障。该标准还使得多重签名脚本更安全地使用，因此在操作成本没有显著增加的情况下，大大提高了安全性。

在钱包软件中实施输出脚本描述符的决定极大地减少了钱包操作的复杂性，并提高了功能集的灵活性。描述符是一种描述脚本的语言，由 Pieter Wuille 编写，并在 Bitcoin Core 中使用。在 River 的钱包软件中，描述符语言在从钱包创建到地址生成的多个环节得到了应用。在描述符之前，钱包之间没有互操作的方式来导入它们所使用的脚本的有用信息。通过使用脚本描述符，River 的钱包能够减少启动对脚本、地址或密钥集的监控所需的信息。每个钱包软件中的钱包都有一个关联的描述符，用于创建脚本。这带来了两个直接的好处：

1. **钱包软件能够使用描述符监控冷钱包，并随后派生新地址。** 在我们的旗舰经纪产品中，River 的客户可以创建新的存款地址，将比特币直接存入安全的多重签名冷钱包中。
2. **创建和导入新钱包非常容易，因为描述符语言可以定义所需的脚本。** River 可以管理许多具有不同脚本的钱包，从而为每个钱包制定独立的安全模型。对于冷钱包，使用 P2WSH 多重签名描述符，而对于热钱包（客户提现），使用 P2WPKH 描述符。独立的钱包使得 River 能够将热钱包中的比特币量保持在绝对最低水平（以降低风险），并更好地管理 UTXO 池以提供提现服务。

使用描述符和 PSBT 标准的决定迄今为止带来了显著的收益，因为它们提供了灵活性和互操作性。这一基础将有助于 River Financial 扩展其钱包基础设施。

{% include references.md %}
[Philip Glazman]: https://github.com/philipglazman
[River Financial]: https://river.com/
[topic psbt]: /en/topics/psbt/
[topic descriptors]: /en/topics/output-script-descriptors/
