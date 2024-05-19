---
layout: post
title: GNN Research - Collecting papers on attack on graph neural network [1 - 25]
date: 2024-05-19 12:14:32
description: sharing 25 papers which propose novel techniques to achieve either attack or defense on graph neural networks.
tags: gnn
categories: research
tabs: true
---

## [1 - Model extraction attacks on graph neural networks: Taxonomy and realization.](https://arxiv.org/abs/2010.12751)

### Abstract

Machine learning models are shown to face a severe threat from Model Extraction Attacks, where a well-trained private model owned by a service provider can be stolen by an attacker pretending as a client. Unfortunately, prior works focus on the models trained over the Euclidean space, e.g., images and texts, while how to extract a GNN model that contains a graph structure and node features is yet to be explored. In this paper, for the first time, we comprehensively investigate and develop model extraction attacks against GNN models. We first systematically formalise the threat modelling in the context of GNN model extraction and classify the adversarial threats into seven categories by considering different background knowledge of the attacker, e.g., attributes and/or neighbour connections of the nodes obtained by the attacker. Then we present detailed methods which utilise the accessible knowledge in each threat to implement the attacks. By evaluating over three real-world datasets, our attacks are shown to extract duplicated models effectively, i.e., 84% - 89% of the inputs in the target domain have the same output predictions as the victim model.

### Code

- [github](https://github.com/TrustworthyGNN/MEA-GNN)

## [2 - Watermarking Graph Neural Networks by Random Graphs](https://arxiv.org/abs/2011.00512)

### Abstract

Many learning tasks require us to deal with graph data which contains rich relational information among elements, leading increasing graph neural network (GNN) models to be deployed in industrial products for improving the quality of service. However, they also raise challenges to model authentication. It is necessary to protect the ownership of the GNN models, which motivates us to present a watermarking method to GNN models in this paper. In the proposed method, an Erdos-Renyi (ER) random graph with random node feature vectors and labels is randomly generated as a trigger to train the GNN to be protected together with the normal samples. During model training, the secret watermark is embedded into the label predictions of the ER graph nodes. During model verification, by activating a marked GNN with the trigger ER graph, the watermark can be reconstructed from the output to verify the ownership. Since the ER graph was randomly generated, by feeding it to a non-marked GNN, the label predictions of the graph nodes are random, resulting in a low false alarm rate (of the proposed work). Experimental results have also shown that, the performance of a marked GNN on its original task will not be impaired. Moreover, it is robust against model compression and fine-tuning, which has shown the superiority and applicability.

### Code

- blank

## [3 - Stealing Links from Graph Neural Networks](https://arxiv.org/abs/2005.02131)

### Abstract

Graph data, such as chemical networks and social networks, may be deemed confidential/private because the data owner often spends lots of resources collecting the data or the data contains sensitive information, e.g., social relationships. Recently, neural networks were extended to graph data, which are known as graph neural networks (GNNs). Due to their superior performance, GNNs have many applications, such as healthcare analytics, recommender systems, and fraud detection. In this work, we propose the first attacks to steal a graph from the outputs of a GNN model that is trained on the graph. Specifically, given a black-box access to a GNN model, our attacks can infer whether there exists a link between any pair of nodes in the graph used to train the model. We call our attacks link stealing attacks. We propose a threat model to systematically characterize an adversary's background knowledge along three dimensions which in total leads to a comprehensive taxonomy of 8 different link stealing attacks. We propose multiple novel methods to realize these 8 attacks. Extensive experiments on 8 real-world datasets show that our attacks are effective at stealing links, e.g., AUC (area under the ROC curve) is above 0.95 in multiple cases. Our results indicate that the outputs of a GNN model reveal rich information about the structure of the graph used to train the model.

### Code

- [github](https://github.com/xinleihe/link_stealing_attack)

## [4 - Node-Level Membership Inference Attacks Against Graph Neural Networks](https://arxiv.org/abs/2102.05429)

### Abstract

Many real-world data comes in the form of graphs, such as social networks and protein structure. To fully utilize the information contained in graph data, a new family of machine learning (ML) models, namely graph neural networks (GNNs), has been introduced. Previous studies have shown that machine learning models are vulnerable to privacy attacks. However, most of the current efforts concentrate on ML models trained on data from the Euclidean space, like images and texts. On the other hand, privacy risks stemming from GNNs remain largely unstudied.
In this paper, we fill the gap by performing the first comprehensive analysis of node-level membership inference attacks against GNNs. We systematically define the threat models and propose three node-level membership inference attacks based on an adversary's background knowledge. Our evaluation on three GNN structures and four benchmark datasets shows that GNNs are vulnerable to node-level membership inference even when the adversary has minimal background knowledge. Besides, we show that graph density and feature similarity have a major impact on the attack's success. We further investigate two defense mechanisms and the empirical results indicate that these defenses can reduce the attack performance but with moderate utility loss.

### Code

- blank

## [5 - Model Stealing Attacks Against Inductive Graph Neural Networks](https://arxiv.org/abs/2112.08331)

### Abstract

Many real-world data come in the form of graphs. Graph neural networks (GNNs), a new family of machine learning (ML) models, have been proposed to fully leverage graph data to build powerful applications. In particular, the inductive GNNs, which can generalize to unseen data, become mainstream in this direction. Machine learning models have shown great potential in various tasks and have been deployed in many real-world scenarios. To train a good model, a large amount of data as well as computational resources are needed, leading to valuable intellectual property. Previous research has shown that ML models are prone to model stealing attacks, which aim to steal the functionality of the target models. However, most of them focus on the models trained with images and texts. On the other hand, little attention has been paid to models trained with graph data, i.e., GNNs. In this paper, we fill the gap by proposing the first model stealing attacks against inductive GNNs. We systematically define the threat model and propose six attacks based on the adversary's background knowledge and the responses of the target models. Our evaluation on six benchmark datasets shows that the proposed model stealing attacks against GNNs achieve promising performance.

### Code

- [github](https://github.com/xinleihe/gnnstealing)

## [6 - Membership Inference Attack on Graph Neural Networks](https://arxiv.org/abs/2110.02631)

## Abstract

Graph Neural Networks (GNNs), which generalize traditional deep neural networks on graph data, have achieved state-of-the-art performance on several graph analytical tasks. We focus on how trained GNN models could leak information about the \emph{member} nodes that they were trained on. We introduce two realistic settings for performing a membership inference (MI) attack on GNNs. While choosing the simplest possible attack model that utilizes the posteriors of the trained model (black-box access), we thoroughly analyze the properties of GNNs and the datasets which dictate the differences in their robustness towards MI attack. While in traditional machine learning models, overfitting is considered the main cause of such leakage, we show that in GNNs the additional structural information is the major contributing factor. We support our findings by extensive experiments on four representative GNN models. To prevent MI attacks on GNN, we propose two effective defenses that significantly decreases the attacker's inference by up to 60% without degradation to the target model's performance. Our code is available at this https URL.

## Code

- [github](https://github.com/iyempissy/rebMIGraph)

## [7 - Quantifying Privacy Leakage in Graph Embedding](https://arxiv.org/abs/2010.00906)

## Abstract

Graph embeddings have been proposed to map graph data to low dimensional space for downstream processing (e.g., node classification or link prediction). With the increasing collection of personal data, graph embeddings can be trained on private and sensitive data. For the first time, we quantify the privacy leakage in graph embeddings through three inference attacks targeting Graph Neural Networks. We propose a membership inference attack to infer whether a graph node corresponding to individual user's data was member of the model's training or not. We consider a blackbox setting where the adversary exploits the output prediction scores, and a whitebox setting where the adversary has also access to the released node embeddings. This attack provides an accuracy up to 28% (blackbox) 36% (whitebox) beyond random guess by exploiting the distinguishable footprint between train and test data records left by the graph embedding. We propose a Graph Reconstruction attack where the adversary aims to reconstruct the target graph given the corresponding graph embeddings. Here, the adversary can reconstruct the graph with more than 80% of accuracy and link inference between two nodes around 30% more confidence than a random guess. We then propose an attribute inference attack where the adversary aims to infer a sensitive attribute. We show that graph embeddings are strongly correlated to node attributes letting the adversary inferring sensitive information (e.g., gender or location).

## Code

- [github](https://github.com/vasishtduddu/GraphLeaks)

## [8 - Inference Attacks Against Graph Neural Networks](https://arxiv.org/abs/2110.02631)

## Abstract

Graph is an important data representation ubiquitously existing in the real world. However, analyzing the graph data is computationally difficult due to its non-Euclidean nature. Graph embedding is a powerful tool to solve the graph analytics problem by transforming the graph data into low-dimensional vectors. These vectors could also be shared with third parties to gain additional insights of what is behind the data. While sharing graph embedding is intriguing, the associated privacy risks are unexplored. In this paper, we systematically investigate the information leakage of the graph embedding by mounting three inference attacks. First, we can successfully infer basic graph properties, such as the number of nodes, the number of edges, and graph density, of the target graph with up to 0.89 accuracy. Second, given a subgraph of interest and the graph embedding, we can determine with high confidence that whether the subgraph is contained in the target graph. For instance, we achieve 0.98 attack AUC on the DD dataset. Third, we propose a novel graph reconstruction attack that can reconstruct a graph that has similar graph structural statistics to the target graph. We further propose an effective defense mechanism based on graph embedding perturbation to mitigate the inference attacks without noticeable performance degradation for graph classification tasks. Our code is available at this https URL.

## Code

- [github](https://github.com/Zhangzhk0819/GNN-Embedding-Leaks)

## [8 - Group Property Inference Attacks Against Graph Neural Networks](https://arxiv.org/abs/2209.01100)

## Abstract

With the fast adoption of machine learning (ML) techniques, sharing of ML models is becoming popular. However, ML models are vulnerable to privacy attacks that leak information about the training data. In this work, we focus on a particular type of privacy attacks named property inference attack (PIA) which infers the sensitive properties of the training data through the access to the target ML model. In particular, we consider Graph Neural Networks (GNNs) as the target model, and distribution of particular groups of nodes and links in the training graph as the target property. While the existing work has investigated PIAs that target at graph-level properties, no prior works have studied the inference of node and link properties at group level yet.
In this work, we perform the first systematic study of group property inference attacks (GPIA) against GNNs. First, we consider a taxonomy of threat models under both black-box and white-box settings with various types of adversary knowledge, and design six different attacks for these settings. We evaluate the effectiveness of these attacks through extensive experiments on three representative GNN models and three real-world graphs. Our results demonstrate the effectiveness of these attacks whose accuracy outperforms the baseline approaches. Second, we analyze the underlying factors that contribute to GPIA's success, and show that the target model trained on the graphs with or without the target property represents some dissimilarity in model parameters and/or model outputs, which enables the adversary to infer the existence of the property. Further, we design a set of defense mechanisms against the GPIA attacks, and demonstrate that these mechanisms can reduce attack accuracy effectively with small loss on GNN model accuracy.

## Code

## [9 - Model Inversion Attacks Against Graph Neural Networks](https://arxiv.org/abs/2209.07807)

## Abstract

Many data mining tasks rely on graphs to model relational structures among individuals (nodes). Since relational data are often sensitive, there is an urgent need to evaluate the privacy risks in graph data. One famous privacy attack against data analysis models is the model inversion attack, which aims to infer sensitive data in the training dataset and leads to great privacy concerns. Despite its success in grid-like domains, directly applying model inversion attacks on non-grid domains such as graph leads to poor attack performance. This is mainly due to the failure to consider the unique properties of graphs. To bridge this gap, we conduct a systematic study on model inversion attacks against Graph Neural Networks (GNNs), one of the state-of-the-art graph analysis tools in this paper. Firstly, in the white-box setting where the attacker has full access to the target GNN model, we present GraphMI to infer the private training graph data. Specifically, in GraphMI, a projected gradient module is proposed to tackle the discreteness of graph edges and preserve the sparsity and smoothness of graph features; a graph auto-encoder module is used to efficiently exploit graph topology, node attributes, and target model parameters for edge inference; a random sampling module can finally sample discrete edges. Furthermore, in the hard-label black-box setting where the attacker can only query the GNN API and receive the classification results, we propose two methods based on gradient estimation and reinforcement learning (RL-GraphMI). Our experimental results show that such defenses are not sufficiently effective and call for more advanced defenses against privacy attacks.

## Code

## [10 - GraphMI: Extracting Private Graph Data from Graph Neural Networks](https://arxiv.org/abs/2106.02820)

## Abstract

As machine learning becomes more widely used for critical applications, the need to study its implications in privacy turns to be urgent. Given access to the target model and auxiliary information, the model inversion attack aims to infer sensitive features of the training dataset, which leads to great privacy concerns. Despite its success in grid-like domains, directly applying model inversion techniques on non-grid domains such as graph achieves poor attack performance due to the difficulty to fully exploit the intrinsic properties of graphs and attributes of nodes used in Graph Neural Networks (GNN). To bridge this gap, we present \textbf{Graph} \textbf{M}odel \textbf{I}nversion attack (GraphMI), which aims to extract private graph data of the training graph by inverting GNN, one of the state-of-the-art graph analysis tools. Specifically, we firstly propose a projected gradient module to tackle the discreteness of graph edges while preserving the sparsity and smoothness of graph features. Then we design a graph auto-encoder module to efficiently exploit graph topology, node attributes, and target model parameters for edge inference. With the proposed methods, we study the connection between model inversion risk and edge influence and show that edges with greater influence are more likely to be recovered. Extensive experiments over several public datasets demonstrate the effectiveness of our method. We also show that differential privacy in its canonical form can hardly defend our attack while preserving decent utility.

## Code

- [github](https://github.com/zaixizhang/GraphMI)

## [11 - ML-Doctor: Holistic Risk Assessment of Inference Attacks Against Machine Learning Models](https://arxiv.org/abs/2102.02551)

## Abstract

Inference attacks against Machine Learning (ML) models allow adversaries to learn sensitive information about training data, model parameters, etc. While researchers have studied, in depth, several kinds of attacks, they have done so in isolation. As a result, we lack a comprehensive picture of the risks caused by the attacks, e.g., the different scenarios they can be applied to, the common factors that influence their performance, the relationship among them, or the effectiveness of possible defenses. In this paper, we fill this gap by presenting a first-of-its-kind holistic risk assessment of different inference attacks against machine learning models. We concentrate on four attacks -- namely, membership inference, model inversion, attribute inference, and model stealing -- and establish a threat model taxonomy.
Our extensive experimental evaluation, run on five model architectures and four image datasets, shows that the complexity of the training dataset plays an important role with respect to the attack's performance, while the effectiveness of model stealing and membership inference attacks are negatively correlated. We also show that defenses like DP-SGD and Knowledge Distillation can only mitigate some of the inference attacks. Our analysis relies on a modular re-usable software, ML-Doctor, which enables ML model owners to assess the risks of deploying their models, and equally serves as a benchmark tool for researchers and practitioners.

## Code

- [github](https://github.com/liuyugeng/ML-Doctor)

## [12 - MemGuard: Defending against Black-Box Membership Inference Attacks via Adversarial Examples](https://arxiv.org/abs/1909.10594)

## Abstract

In a membership inference attack, an attacker aims to infer whether a data sample is in a target classifier's training dataset or not. Specifically, given a black-box access to the target classifier, the attacker trains a binary classifier, which takes a data sample's confidence score vector predicted by the target classifier as an input and predicts the data sample to be a member or non-member of the target classifier's training dataset. Membership inference attacks pose severe privacy and security threats to the training dataset. Most existing defenses leverage differential privacy when training the target classifier or regularize the training process of the target classifier. These defenses suffer from two key limitations: 1) they do not have formal utility-loss guarantees of the confidence score vectors, and 2) they achieve suboptimal privacy-utility tradeoffs.
In this work, we propose MemGuard, the first defense with formal utility-loss guarantees against black-box membership inference attacks. Instead of tampering the training process of the target classifier, MemGuard adds noise to each confidence score vector predicted by the target classifier. Our key observation is that attacker uses a classifier to predict member or non-member and classifier is vulnerable to adversarial examples. Based on the observation, we propose to add a carefully crafted noise vector to a confidence score vector to turn it into an adversarial example that misleads the attacker's classifier. Our experimental results on three datasets show that MemGuard can effectively defend against membership inference attacks and achieve better privacy-utility tradeoffs than existing defenses. Our work is the first one to show that adversarial examples can be used as defensive mechanisms to defend against membership inference attacks.

## Code

- [github](https://github.com/jinyuan-jia/memguard)

## [13 - Adversarial Attacks on Neural Networks for Graph Data](https://arxiv.org/abs/1805.07984)

## Abstract

Deep learning models for graphs have achieved strong performance for the task of node classification. Despite their proliferation, currently there is no study of their robustness to adversarial attacks. Yet, in domains where they are likely to be used, e.g. the web, adversaries are common. Can deep learning models for graphs be easily fooled? In this work, we introduce the first study of adversarial attacks on attributed graphs, specifically focusing on models exploiting ideas of graph convolutions. In addition to attacks at test time, we tackle the more challenging class of poisoning/causative attacks, which focus on the training phase of a machine learning model. We generate adversarial perturbations targeting the node's features and the graph structure, thus, taking the dependencies between instances in account. Moreover, we ensure that the perturbations remain unnoticeable by preserving important data characteristics. To cope with the underlying discrete domain we propose an efficient algorithm Nettack exploiting incremental computations. Our experimental study shows that accuracy of node classification significantly drops even when performing only few perturbations. Even more, our attacks are transferable: the learned attacks generalize to other state-of-the-art node classification models and unsupervised approaches, and likewise are successful even when only limited knowledge about the graph is given.

## Code

- [github](https://github.com/danielzuegner/nettack)

## [14 - Adversarial Attack on Graph Structured Data]

## Abstract

Deep learning on graph structures has shown exciting results in various applications. However, few attentions have been paid to the robustness of such models, in contrast to numerous research work for image or text adversarial attack and defense. In this paper, we focus on the adversarial attacks that fool the model by modifying the combinatorial structure of data. We first propose a reinforcement learning based attack method that learns the generalizable attack policy, while only requiring prediction labels from the target classifier. Also, variants of genetic algorithms and gradient methods are presented in the scenario where prediction confidence or gradients are available. We use both synthetic and real-world data to show that, a family of Graph Neural Network models are vulnerable to these attacks, in both graph-level and node-level classification tasks. We also show such attacks can be used to diagnose the learned classifiers.

## Code

- [github](https://github.com/Hanjun-Dai/graph_adversarial_attack)

## [15 - Adversarial Examples on Graph Data: Deep Insights into Attack and Defense]

## Abstract

Graph deep learning models, such as graph convolutional networks (GCN) achieve remarkable performance for tasks on graph data. Similar to other types of deep models, graph deep learning models often suffer from adversarial attacks. However, compared with non-graph data, the discrete features, graph connections and different definitions of imperceptible perturbations bring unique challenges and opportunities for the adversarial attacks and defenses for graph data. In this paper, we propose both attack and defense techniques. For attack, we show that the discreteness problem could easily be resolved by introducing integrated gradients which could accurately reflect the effect of perturbing certain features or edges while still benefiting from the parallel computations. For defense, we observe that the adversarially manipulated graph for the targeted attack differs from normal graphs statistically. Based on this observation, we propose a defense approach which inspects the graph and recovers the potential adversarial perturbations. Our experiments on a number of datasets show the effectiveness of the proposed methods.

## Code

- [github](https://github.com/stellargraph/stellargraph)

## [16 - Topology Attack and Defense for Graph Neural Networks: An Optimization Perspective](https://arxiv.org/abs/1906.04214)

## Abstract

Graph neural networks (GNNs) which apply the deep neural networks to graph data have achieved significant performance for the task of semi-supervised node classification. However, only few work has addressed the adversarial robustness of GNNs. In this paper, we first present a novel gradient-based attack method that facilitates the difficulty of tackling discrete graph data. When comparing to current adversarial attacks on GNNs, the results show that by only perturbing a small number of edge perturbations, including addition and deletion, our optimization-based attack can lead to a noticeable decrease in classification performance. Moreover, leveraging our gradient-based attack, we propose the first optimization-based adversarial training for GNNs. Our method yields higher robustness against both different gradient based and greedy attack methods without sacrificing classification accuracy on original graph.

## Code

- [github](https://github.com/KaidiXu/GCN_ADV_Train)

## [17 - Adversarial Attacks on Node Embeddings via Graph Poisoning](https://arxiv.org/abs/1809.01093)

## Abstract

The goal of network representation learning is to learn low-dimensional node embeddings that capture the graph structure and are useful for solving downstream tasks. However, despite the proliferation of such methods, there is currently no study of their robustness to adversarial attacks. We provide the first adversarial vulnerability analysis on the widely used family of methods based on random walks. We derive efficient adversarial perturbations that poison the network structure and have a negative effect on both the quality of the embeddings and the downstream tasks. We further show that our attacks are transferable since they generalize to many models and are successful even when the attacker is restricted.

## Code

- [github](https://github.com/abojchevski/node_embedding_attack)

## [18 - Adversarial Attacks on Graph Neural Networks via Meta Learning]

## Abstract

Deep learning models for graphs have advanced the state of the art on many tasks. Despite their recent success, little is known about their robustness. We investigate training time attacks on graph neural networks for node classification that perturb the discrete graph structure. Our core principle is to use meta-gradients to solve the bilevel problem underlying training-time attacks, essentially treating the graph as a hyperparameter to optimize. Our experiments show that small graph perturbations consistently lead to a strong decrease in performance for graph convolutional networks, and even transfer to unsupervised embeddings. Remarkably, the perturbations created by our algorithm can misguide the graph neural networks such that they perform worse than a simple baseline that ignores all relational information. Our attacks do not assume any knowledge about or access to the target classifiers.

## Code

- [github](https://github.com/danielzuegner/gnn-meta-attack)

## [19 - PeerNets: Exploiting Peer Wisdom Against Adversarial Attacks](https://arxiv.org/abs/1806.00088)

## Abstract

Deep learning systems have become ubiquitous in many aspects of our lives. Unfortunately, it has been shown that such systems are vulnerable to adversarial attacks, making them prone to potential unlawful uses. Designing deep neural networks that are robust to adversarial attacks is a fundamental step in making such systems safer and deployable in a broader variety of applications (e.g. autonomous driving), but more importantly is a necessary step to design novel and more advanced architectures built on new computational paradigms rather than marginally building on the existing ones. In this paper we introduce PeerNets, a novel family of convolutional networks alternating classical Euclidean convolutions with graph convolutions to harness information from a graph of peer samples. This results in a form of non-local forward propagation in the model, where latent features are conditioned on the global structure induced by the graph, that is up to 3 times more robust to a variety of white- and black-box adversarial attacks compared to conventional architectures with almost no drop in accuracy.

## Code

- [github](https://github.com/tantara/PeerNets-pytorch)

## [20 - Certifiable Robustness to Graph Perturbations]

## Abstract

Despite the exploding interest in graph neural networks there has been little effort to verify and improve their robustness. This is even more alarming given recent findings showing that they are extremely vulnerable to adversarial attacks on both the graph structure and the node attributes. We propose the first method for verifying certifiable (non-)robustness to graph perturbations for a general class of models that includes graph neural networks and label/feature propagation. By exploiting connections to PageRank and Markov decision processes our certificates can be efficiently (and under many threat models exactly) computed. Furthermore, we investigate robust training procedures that increase the number of certifiably robust nodes while maintaining or improving the clean predictive accuracy.

## Code

- [github](https://github.com/abojchevski/graph_cert)

## [21 - A Unified Framework for Data Poisoning Attack to Graph-based Semi-supervised Learning](https://arxiv.org/abs/1910.14147)

## Abstract

In this paper, we proposed a general framework for data poisoning attacks to graph-based semi-supervised learning (G-SSL). In this framework, we first unify different tasks, goals, and constraints into a single formula for data poisoning attack in G-SSL, then we propose two specialized algorithms to efficiently solve two important cases --- poisoning regression tasks under ℓ2-norm constraint and classification tasks under ℓ0-norm constraint. In the former case, we transform it into a non-convex trust region problem and show that our gradient-based algorithm with delicate initialization and update scheme finds the (globally) optimal perturbation. For the latter case, although it is an NP-hard integer programming problem, we propose a probabilistic solver that works much better than the classical greedy method. Lastly, we test our framework on real datasets and evaluate the robustness of G-SSL algorithms. For instance, on the MNIST binary classification problem (50000 training data with 50 labeled), flipping two labeled data is enough to make the model perform like random guess (around 50\% error).

## Code

## [22 - GNNGuard: Defending Graph Neural Networks against Adversarial Attacks](https://arxiv.org/abs/2006.08149)

## Abstract

Deep learning methods for graphs achieve remarkable performance across a variety of domains. However, recent findings indicate that small, unnoticeable perturbations of graph structure can catastrophically reduce performance of even the strongest and most popular Graph Neural Networks (GNNs). Here, we develop GNNGuard, a general algorithm to defend against a variety of training-time attacks that perturb the discrete graph structure. GNNGuard can be straight-forwardly incorporated into any GNN. Its core principle is to detect and quantify the relationship between the graph structure and node features, if one exists, and then exploit that relationship to mitigate negative effects of the attack.GNNGuard learns how to best assign higher weights to edges connecting similar nodes while pruning edges between unrelated nodes. The revised edges allow for robust propagation of neural messages in the underlying GNN. GNNGuard introduces two novel components, the neighbor importance estimation, and the layer-wise graph memory, and we show empirically that both components are necessary for a successful defense. Across five GNNs, three defense methods, and five datasets,including a challenging human disease graph, experiments show that GNNGuard outperforms existing defense approaches by 15.3% on average. Remarkably, GNNGuard can effectively restore state-of-the-art performance of GNNs in the face of various adversarial attacks, including targeted and non-targeted attacks, and can defend against attacks on heterophily graphs.

## Code

- [github](https://github.com/mims-harvard/GNNGuard)

## [23 - Robust Graph Convolutional Networks Against Adversarial Attacks](https://github.com/ZW-ZHANG/RobustGCN)

## Abstract

Graph Convolutional Networks (GCNs) are an emerging type of neural network model on graphs which have achieved state-ofthe-art performance in the task of node classification. However, recent studies show that GCNs are vulnerable to adversarial attacks, i.e. small deliberate perturbations in graph structures and node attributes, which poses great challenges for applying GCNs to real world applications. How to enhance the robustness of GCNs remains a critical open problem. To address this problem, we propose Robust GCN (RGCN), a novel model that “fortifies” GCNs against adversarial attacks. Specifically, instead of representing nodes as vectors, our method adopts Gaussian distributions as the hidden representations of nodes in each convolutional layer. In this way, when the graph is attacked, our model can automatically absorb the effects of adversarial changes in the variances of the Gaussian distributions. Moreover, to remedy the propagation of adversarial attacks in GCNs, we propose a variance-based attention mechanism, i.e. assigning different weights to node neighborhoods according to their variances when performing convolutions. Extensive experimental results demonstrate that our proposed method can effectively improve the robustness of GCNs. On three benchmark graphs, our RGCN consistently shows a substantial gain in node classification accuracy compared with state-of-the-art GCNs against various adversarial attack strategies.

## Code

- [github](https://github.com/ZW-ZHANG/RobustGCN)

## [24 - A Restricted Black-Box Adversarial Framework Towards Attacking Graph Embedding Models](https://arxiv.org/abs/1908.01297)

## Abstract

With the great success of graph embedding model on both academic and industry area, the robustness of graph embedding against adversarial attack inevitably becomes a central problem in graph learning domain. Regardless of the fruitful progress, most of the current works perform the attack in a white-box fashion: they need to access the model predictions and labels to construct their adversarial loss. However, the inaccessibility of model predictions in real systems makes the white-box attack impractical to real graph learning system. This paper promotes current frameworks in a more general and flexible sense -- we demand to attack various kinds of graph embedding model with black-box driven. To this end, we begin by investigating the theoretical connections between graph signal processing and graph embedding models in a principled way and formulate the graph embedding model as a general graph signal process with corresponding graph filter. As such, a generalized adversarial attacker: GF-Attack is constructed by the graph filter and feature matrix. Instead of accessing any knowledge of the target classifiers used in graph embedding, GF-Attack performs the attack only on the graph filter in a black-box attack fashion. To validate the generalization of GF-Attack, we construct the attacker on four popular graph embedding models. Extensive experimental results validate the effectiveness of our attacker on several benchmark datasets. Particularly by using our attack, even small graph perturbations like one-edge flip is able to consistently make a strong attack in performance to different graph embedding models.

## Code

- [github](https://github.com/SwiftieH/GFAttack)

## [25 - All You Need Is Low (Rank): Defending Against Adversarial Attacks on Graphs](https://dl.acm.org/doi/10.1145/3336191.3371789)

## Abstract

Recent studies have demonstrated that machine learning approaches like deep learning methods are easily fooled by adversarial attacks. Recently, a highly-influential study examined the impact of adversarial attacks on graph data and demonstrated that graph embedding techniques are also vulnerable to adversarial attacks. Fake users on social media and fake product reviews are examples of perturbations in graph data that are realistic counterparts of the adversarial models proposed. Graphs are widely used in a variety of domains and it is highly important to develop graph analysis techniques that are robust to adversarial attacks. One of the recent studies on generating adversarial attacks for graph data is Nettack. The Nettack model has shown to be very successful in deceiving the Graph Convolutional Network (GCN) model. Nettack is also transferable to other node classification approaches e.g. node embeddings. In this paper, we explore the properties of Nettack perturbations, in search for effective defenses against them. Our first finding is that Nettack demonstrates a very specific behavior in the spectrum of the graph: only high-rank (low-valued) singular components of the graph are affected. Following that insight, we show that a low-rank approximation of the graph, that uses only the top singular components for its reconstruction, can greatly reduce the effects of Nettack and boost the performance of GCN when facing adversarial attacks. Indicatively, on the CiteSeer dataset, our proposed defense mechanism is able to reduce the success rate of Nettack from 98% to 36%. Furthermore, we show that tensor-based node embeddings, which by default project the graph into a low-rank subspace, are robust against Nettack perturbations. Lastly, we propose LowBlow, a low-rank adversarial attack which is able to affect the classification performance of both GCN and tensor-based node embeddings and we show that the low-rank attack is noticeable and making it unnoticeable results in a high-rank attack.

## Code

<!--
## some tools

- connectedpapers -->
