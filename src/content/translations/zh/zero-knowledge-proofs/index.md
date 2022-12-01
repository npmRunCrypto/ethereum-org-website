---
title: 零知识证明
description: 针对初学者的零知识证明的非技术性介绍。
lang: zh
---

## 什么是零知识证明？ {#what-are-zk-proofs}

零知识证明是一种在不暴露陈述本身的情况下证明陈述有效性的方法。 “证明者”是试图证明声明的一方，而“验证者”负责验证声明。

零知识证明最早出现在 1985 年的一篇论文中，“[交互式证明系统的知识复杂性](http://people.csail.mit.edu/silvio/Selected%20Scientific%20Papers/Proof%20Systems/The_Knowledge_Complexity_Of_Interactive_Proof_Systems.pdf) ”，它提供了当今广泛使用的零知识证明的定义：

> 零知识协议是一种通过一方（证明者）可以向另一方（验证者）证明某事是真实的，除了这个特定陈述是真实的事实之外，不会透露任何信息的方法。

多年来，零知识证明得到了改进，现在它们被用于多个现实世界的应用中。

## 为什么我们需要零知识证明？ {#why-zero-knowledge-proofs-are-important}

零知识证明代表了应用密码学的突破，因为它们承诺提高个人信息的安全性。考虑如何向另一方（例如，服务提供商）证明一项声明（例如，“我是 X 国家/地区的公民”）。您需要提供“证据”来支持您的说法，例如国民护照或驾照。

但这种方法存在问题，主要是缺乏隐私。与第三方服务共享的个人身份信息 (PII) 存储在容易受到黑客攻击的中央数据库中。随着身份盗窃成为一个关键问题，人们呼吁采用更多的隐私保护方式来共享敏感信息。

零知识证明通过消除披露信息来证明声明有效性的需要来解决这个问题。零知识协议使用声明（称为“见证”）作为输入来生成其有效性的简洁证明。这个证明提供了一个强有力的保证，即一个陈述是真实的，而不会暴露创建它所使用的信息。

回到我们之前的例子，你需要证明你的公民身份的唯一证据是零知识证明。验证者只需检查证明的某些属性是否成立，就可以确信基础陈述也成立。

## 零知识证明如何工作？ {#how-do-zero-knowledge-proofs-work}

零知识证明允许您证明陈述的真实性，而无需共享陈述的内容或透露您是如何发现真相的。为了使这成为可能，零知识协议依赖于将一些数据作为输入并返回“真”或“假”作为输出的算法。

零知识协议必须满足以下条件：

1. **完备性**：如果输入有效，零知识协议总是返回“真”。因此，如果基础陈述是真实的，并且证明者和验证者诚实行事，则证明可以被接受。

2. **健全性**：如果输入无效，理论上不可能骗过零知识协议返回‘true’。因此，说谎的证明者无法欺骗诚实的验证者相信无效的陈述是有效的（除非概率很小）。

3. **零知识**：验证者除了陈述的有效性或虚假性之外，对陈述一无所知（他们对陈述“零知识”）。此要求还阻止验证者从证明中导出原始输入（语句的内容）。

在基本形式中，零知识证明由三个要素组成：**见证**、**挑战**和**响应**。

- **见证**：通过零知识证明，证明者想要证明一些隐藏信息的知识。秘密信息是证明的“证人”，证明者对证人的假设知识建立了一组问题，这些问题只能由了解信息的一方回答。因此，证明者通过随机选择一个问题、计算答案并将其发送给验证者来开始证明过程。

- **挑战**：验证者从集合中随机选择另一个问题，并要求证明者回答。

- **响应**：证明者接受问题，计算答案，返回给验证者。证明者的回应允许验证者检查前者是否真的可以访问见证人。为了确保证明者不会盲目猜测并偶然得到正确答案，验证者会选择更多的问题来提问。通过多次重复这种交互，证明者伪造证人知识的可能性显着下降，直到验证者满意为止。

以上描述了“交互式零知识证明”的结构。早期的零知识协议使用交互式证明，其中验证语句的有效性需要证明者和验证者之间的来回通信。

Jean-Jacques Quisquater 著名的阿里巴巴洞穴故事是说明交互式证明如何工作的一个很好的例子。在故事中，Peggy（证明者）想向 Victor（验证者）证明她知道打开魔法门的秘密短语而不泄露该短语。

### 非交互式零知识证明 {#non-interactive-zero-knowledge-proofs}

虽然具有革命性，但交互式证明的用处有限，因为它需要两方随时可用并反复交互。即使验证者确信证明者是诚实的，该证明也无法用于独立验证（计算新证明需要证明者和验证者之间的一组新消息）。

为了解决这个问题，Manuel Blum、Paul Feldman 和 Silvio Micali 提出了第一个非交互式零知识证明，其中证明者和验证者拥有共享密钥。这允许证明者在不提供信息本身的情况下证明他们对某些信息的了解（即见证）。

与交互式证明不同，非交互式证明只需要参与者（证明者和验证者）之间进行一轮通信。证明者将秘密信息传递给特殊算法以计算零知识证明。该证明被发送给验证者，验证者使用另一种算法检查证明者是否知道秘密信息。

非交互式证明减少了证明者和验证者之间的通信，使 ZK 证明更加高效。此外，一旦生成了证明，其他任何人（可以访问共享密钥和验证算法）都可以进行验证。

非交互式证明代表了零知识技术的突破，并推动了当今使用的证明系统的发展。我们在下面讨论这些证明类型：

### 零知识证明的类型 {#types-of-zero-knowledge-proofs}

#### ZK-SNARKs {#zk-snarks}

ZK-SNARK 是 Zero-Knowledge Succinct Non-Interactive Argument of Knowledge 的缩写。 ZK-SNARK 协议具有以下特点：

- **零知识**：验证者可以在不知道语句的任何其他信息的情况下验证语句的完整性。验证者对声明的唯一了解是它是真还是假。

- **简洁**：零知识证明比见证小，可以快速验证。

- **非交互式**：证明是“非交互式”的，因为证明者和验证者只交互一次，不像交互式证明需要多轮通信。

- **论证**：证明满足“可靠性”要求，因此作弊的可能性极小。

- **(Of) Knowledge**：如果不访问秘密信息（witness），则无法构建零知识证明。对于没有见证人的证明者来说，即使不是不可能，也很难计算出有效的零知识证明。

前面提到的“共享密钥”是指证明者和验证者同意在生成和验证证明时使用的公共参数。生成公共参数（统称为公共参考字符串 (CRS)）是一项敏感操作，因为它对协议的安全性很重要。如果用于生成 CRS 的熵（随机性）落入不诚实的证明者手中，他们就可以计算出错误证明。

多方计算（MPC）是一种降低生成公共参数风险的方法。多方参与可信设置仪式，其中每个人贡献一些随机值来生成 CRS。只要一个诚实的一方破坏了他们的熵部分，ZK-SNARK 协议就会保持计算稳健性。

可信设置要求用户信任参数生成的参与者。然而，ZK-STARKs 的开发使得证明协议能够在不受信任的设置下工作。

#### ZK-STARKs {#zk-starks}

ZK-STARK 是 Zero-Knowledge Scalable Transparent Argument of Knowledge 的缩写。 ZK-STARKs 类似于 ZK-SNARKs，除了它们是：

- **可扩展性**：当见证规模较大时，ZK-STARK 在生成和验证证明方面比 ZK-SNARK 更快。使用 STARK 证明，证明者和验证者的时间只会随着见证的增长而略有增加（SNARK 证明者和验证者的时间随着见证者的规模线性增加）。

- **透明**：ZK-STARK 依靠可公开验证的随机性来生成用于证明和验证的公共参数，而不是可信设置。因此，与 ZK-SNARK 相比，它们更加透明。

ZK-STARKs 产生比 ZK-SNARKs 更大的证明，这意味着它们通常具有更高的验证开销。但是，在某些情况下（例如证明大型数据集），ZK-STARK 可能比 ZK-SNARK 更具成本效益。

## 零知识证明的用例 {#use-cases-for-zero-knowledge-proofs}

### 匿名支付 {#anonymous-payments}

信用卡支付通常对多方可见，包括支付提供商、银行和其他相关方（例如政府机构）。虽然金融监督有利于识别非法活动，但它也损害了普通公民的隐私。

加密货币旨在为用户提供一种进行私人、点对点交易的方式。但大多数加密货币交易在公共区块链上都是公开可见的。用户身份通常是假名的，并且要么故意链接到真实世界的身份（例如，通过在 Twitter 或 GitHub 个人资料中包含 ETH 地址），要么可以使用基本的链上和链下数据分析与真实世界的身份相关联。

有专为完全匿名交易而设计的特定“隐私币”。以隐私为中心的区块链，如 ZCash 和门罗币，屏蔽交易细节，包括发送者/接收者地址、资产类型、数量和交易时间表。

通过将零知识技术融入协议，以隐私为中心的区块链网络允许节点在无需访问交易数据的情况下验证交易。

零知识证明也被应用于公共区块链上的匿名交易。一个例子是 Tornado Cash，这是一种去中心化的非托管服务，允许用户在以太坊上进行私人交易。 Tornado Cash 使用零知识证明来混淆交易细节并保证财务隐私。不幸的是，因为这些是“选择加入”的隐私工具，所以它们与非法活动有关。为了克服这个问题，隐私最终必须成为公共区块链的默认设置。

### 身份保护{#identity-protection}

当前的身份管理系统将个人信息置于危险之中。零知识证明可以帮助个人验证身份，同时保护敏感细节。

零知识证明在去中心化身份的背景下特别有用。去中心化身份（也称为“自我主权身份”）使个人能够控制对个人标识符的访问。在不透露您的税号或护照详细信息的情况下证明您的公民身份是零知识技术如何实现去中心化身份的一个很好的例子。

### 身份验证{#authentication}

使用在线服务需要证明您的身份和访问这些平台的权利。这通常需要提供个人信息，例如姓名、电子邮件地址、出生日期等。您可能还需要记住长密码，否则可能会失去访问权限。

然而，零知识证明可以简化平台和用户的身份验证。一旦使用公共输入（例如，证明用户是平台成员的数据）和私人输入（例如，用户的详细信息）生成了 ZK 证明，用户可以在需要访问时简单地出示它以验证其身份服务。这改善了用户体验，并使组织无需存储大量用户信息。

### 可验证计算 {#verifiable-computation}

可验证计算是零知识技术改进区块链设计的另一种应用。可验证计算允许我们将计算外包给另一个实体，同时保持可验证的结果。该实体将结果连同证明程序已正确执行的证据一起提交。

可验证计算对于在不降低安全性的情况下提高区块链处理速度至关重要。理解这一点需要了解扩展以太坊的提议解决方案的差异。

[链上扩展解决方案](/developers/docs/scaling/#on-chain-scaling)，例如分片等需要对区块链的基础层进行大量修改。然而，这种方法非常复杂，实施中的错误可能会破坏以太坊的安全模型。

[链下扩展解决方案](/developers/docs/scaling/#off-chain-scaling)不需要重新设计核心以太坊协议。相反，他们依靠外包计算模型来提高以太坊基础层的吞吐量。

这是它在实践中的工作原理：

- 以太坊不是处理每笔交易，而是将执行卸载到一个单独的链上。

- 处理交易后，另一条链返回结果以应用于以太坊的状态。

这里的好处是以太坊不需要执行任何操作，只需要将外包计算的结果应用到它的状态。这减少了网络拥塞并提高了交易速度（链下协议优化以加快执行速度）。

链需要一种方法来验证链下交易而不重新执行它们，否则链下执行的价值就会丢失。

这就是可验证计算发挥作用的地方。当一个节点在以太坊之外执行交易时，它会提交一个零知识证明来证明链下执行的正确性。该证明（称为[有效性证明](/glossary/#validity-proof)）保证交易有效，允许以太坊将结果应用于其状态——无需等待任何人对其提出异议。

[零知识汇总](/developers/docs/scaling/zk-rollups)和[验证](/developers/docs/scaling/validium/)是两种链下扩展解决方案，它们使用有效性证明来提供安全的可扩展性。这些协议在链下执行数千笔交易，并提交证明以在以太坊上进行验证。一旦证明得到验证，这些结果就可以立即应用，从而允许以太坊处理更多交易，而无需增加基础层的计算。

## 使用零知识证明的缺点 {#drawbacks-of-using-zero-knowledge-proofs}

### 硬件成本 {#hardware-costs}

生成零知识证明涉及非常复杂的计算，最好在专用机器上执行。由于这些机器价格昂贵，它们通常是普通人买不起的。此外，想要使用零知识技术的应用程序必须考虑硬件成本——这可能会增加最终用户的成本。

### 证明验证成本 {#proof-verification-costs}

验证证明还需要复杂的计算，并增加了在应用程序中实施零知识技术的成本。这个成本在证明计算的上下文中特别相关。例如，ZK-rollups 支付约 500,000 gas 来验证以太坊上的单个 ZK-SNARK 证明，而 ZK-STARKs 需要更高的费用。

### 信任假设 {#trust-assumptions}

在 ZK-SNARK 中，公共参考字符串（公共参数）生成一次，可供希望参与零知识协议的各方重复使用。公共参数是通过可信的设置仪式创建的，参与者被认为是诚实的。

但用户确实没有办法评估参与者的诚实度，用户必须相信开发人员的话。 ZK-STARK 没有信任假设，因为生成字符串时使用的随机性是可公开验证的。与此同时，研究人员正在为 ZK-SNARKs 进行非可信设置，以提高证明机制的安全性。

### 量子计算威胁 {#quantum-computing-threats}

ZK-SNARK 使用椭圆曲线密码学 (ECDSA) 进行加密。虽然 ECDSA 算法目前是安全的，但未来量子计算机的发展可能会打破其安全模型。

ZK-STARK 被认为不受量子计算的威胁，因为它使用抗碰撞哈希进行加密。与椭圆曲线密码学中使用的公私密钥对不同，抗碰撞散列更难被量子计算算法破解。

## 进一步阅读 {#further-reading}
- [计算机科学家分5个难度解释一个概念](https://www.youtube.com/watch?v=fOGdb1CTu5c) - WIRED - 有线 YouTube 频道
- [SNARKs vs. STARKS vs. Recursive SNARKs](https://www.alchemy.com/overviews/snarks-vs-starks) — Alchemy Overviews
- [零知识证明：改善区块链上的隐私](https://www.altoros.com/blog/zero-knowledge-proof-improving-privacy-for-a-blockchain/) — Dmitry Lavrenov
- [zk-SNARKs——一个现实的零知识示例和深入研究](https://medium.com/coinmonks/zk-snarks-a-realistic-zero-knowledge-example-and-deep-dive-c5e6eaa7131c) —— Adam Luciano
- [ZK-STARKs — 创建可验证的信任，即使是针对量子计算机](https://medium.com/coinmonks/zk-starks-create-verifiable-trust-even-against-quantum-computers-dd9c6a2bb13d) — Adam Luciano
- [zk-SNARKs 如何成为可能的大致介绍](https://vitalik.ca/general/2021/01/26/snarks.html)  — Vitalik Buterin
- [什么是零知识证明及其在区块链中的作用？](https://www.leewayhertz.com/zero-knowledge-proof-and-blockchain/) — LeewayHertz