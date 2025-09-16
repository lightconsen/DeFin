# zk-SNARKs

zk-SNARKs的构建主要依赖于以下几项核心理论和技术：

1. **零知识证明（Zero-Knowledge Proof, ZKP）的概念**
   * **提出者**：Shafi Goldwasser, Silvio Micali, Charles Rackoff
   * **论文**：**《The Knowledge Complexity of Interactive Proof Systems》** (1985)
   * **内容**：这篇开创性的论文首次提出了**零知识证明**的概念，并奠定了交互式证明系统的理论基础。它定义了什么是“知识复杂性”，并展示了如何在不泄露任何知识的情况下证明一个陈述的真实性。
2. **算术化（Arithmetization）**
   * 这是将计算问题转化为多项式或算术电路的过程，是构建zk-SNARK的第一步。虽然这不是某一篇论文单独提出的，但它是整个领域的基础。
   * **后续研究**：如何更高效地将程序转换为约束系统（如R1CS）和多项式（如QAP）是多篇论文的核心内容。
3. **多项式承诺方案（Polynomial Commitment Scheme）**
   * 多项式承诺是zk-SNARKs能够实现“简洁性”（Succinctness）的关键。它允许证明者对一个多项式进行承诺，然后可以在一个点上揭示其估值并提供证明，而无需暴露整个多项式。
   * **KZG承诺（又称Kate承诺）**：基于配对的双线性映射特性，是早期zk-SNARKs（如Groth16）常用的承诺方案。
   * **提出者**：Aniket Kate, Gregory M. Zaverucha, Ian Goldberg
   * **论文**：**《Constant-Size Commitments to Polynomials and Their Applications》** (2010)
   * **其他方案**：后续也发展出了其他不依赖配对的可选方案，如基于**离散对数**的**Bulletproofs**（内部乘积论证），以及基于哈希函数的**FRI**（用于zk-STARKs）。
4. **椭圆曲线配对（Elliptic Curve Pairings）**
   * 配对函数（如Weil配对、Tate配对）是早期zk-SNARKs（如Groth16）实现其密码学魔力的关键工具，它允许在加密数据之上进行有限形式的计算（双线性映射）。
   * **双线性映射**：使得 $e(g^a, h^b) = e(g, h)^{ab}$ 成立，这是验证过程中能够校验多项式等式成立的基础。
   * 许多论文在此基础上构建了具体的协议，例如Boneh-Lynn-Shacham（BLS）签名方案也利用了配对特性。
5. **随机预言机模型（Random Oracle Model）与非交互化**
   * **Fiat-Shamir启发式（Fiat-Shamir Heuristic）** 是一种将**交互式**证明协议转换为**非交互式**（Non-Interactive）协议的方法。证明者使用 cryptographic hash function 来模拟验证者的挑战。
   * **提出者**：Amos Fiat, Adi Shamir
   * **论文**：**《How to Prove Yourself: Practical Solutions to Identification and Signature Problems》** (1986)
   * **内容**：虽然这篇论文主要关注身份识别和签名，但其提出的Fiat-Shamir启发式被广泛应用于后续的零知识证明系统中，以实现非交互性。
6. **可满足性问题的论证系统（Argument Systems for Satisfiability）**
   * 最终的zk-SNARKs协议是将上述所有组件组合起来，为NP问题（特别是电路可满足性问题）构建具体的论证系统。
   * **Pinocchio协议**：一个里程碑式的工作，展示了如何为通用计算构建高效的zk-SNARK。
   * **提出者**：Bryan Parno, Craig Gentry, Jon Howell, Mariana Raykova
   * **论文**：**《Pinocchio: Nearly Practical Verifiable Computation》** (2013)
   * **Groth16**：目前最常用且性能最优的zk-SNARK方案之一，尤其在区块链领域应用广泛。
   * **提出者**：Jens Groth
   * **论文**：**《On the Size of Pairing-Based Non-interactive Arguments》** (2016)
   * **PLONK**：另一种流行的zk-SNARK方案，其最大优势在于支持**通用可信设置**（Universal Trusted Setup），意味着多个应用程序可以共享同一个可信设置。
   * **提出者**：Ariel Gabizon, Zachary J. Williamson, Oana Ciobotaru
   * **论文**：**《PLONK: Permutations over Lagrange-bases for Oecumenical Noninteractive arguments of Knowledge》** (2019)
