---
layout: post
title: GNN Research - Collecting papers on defense on graph neural network [26 - 50]
date: 2024-05-20 12:14:32
description: sharing 25 papers which propose novel techniques to achieve either attack or defense on graph neural networks.
tags: gnn
categories: research
tabs: true
---

## [26 - Group Property Inference Attacks Against Graph Neural Networks](https://arxiv.org/abs/2209.01100)

### Abstract

With the fast adoption of machine learning (ML) techniques, sharing of ML models is becoming popular. However, ML models are vulnerable to privacy attacks that leak information about the training data. In this work, we focus on a particular type of privacy attacks named property inference attack (PIA) which infers the sensitive properties of the training data through the access to the target ML model. In particular, we consider Graph Neural Networks (GNNs) as the target model, and distribution of particular groups of nodes and links in the training graph as the target property. While the existing work has investigated PIAs that target at graph-level properties, no prior works have studied the inference of node and link properties at group level yet.
In this work, we perform the first systematic study of group property inference attacks (GPIA) against GNNs. First, we consider a taxonomy of threat models under both black-box and white-box settings with various types of adversary knowledge, and design six different attacks for these settings. We evaluate the effectiveness of these attacks through extensive experiments on three representative GNN models and three real-world graphs. Our results demonstrate the effectiveness of these attacks whose accuracy outperforms the baseline approaches. Second, we analyze the underlying factors that contribute to GPIA's success, and show that the target model trained on the graphs with or without the target property represents some dissimilarity in model parameters and/or model outputs, which enables the adversary to infer the existence of the property. Further, we design a set of defense mechanisms against the GPIA attacks, and demonstrate that these mechanisms can reduce attack accuracy effectively with small loss on GNN model accuracy.

### Code

## [27 - Defending Graph Convolutional Networks against Dynamic Graph Perturbations via Bayesian Self-supervision](https://arxiv.org/abs/2203.03762)

### Abstract

In recent years, plentiful evidence illustrates that Graph Convolutional Networks (GCNs) achieve extraordinary accomplishments on the node classification task. However, GCNs may be vulnerable to adversarial attacks on label-scarce dynamic graphs. Many existing works aim to strengthen the robustness of GCNs; for instance, adversarial training is used to shield GCNs against malicious perturbations. However, these works fail on dynamic graphs for which label scarcity is a pressing issue. To overcome label scarcity, self-training attempts to iteratively assign pseudo-labels to highly confident unlabeled nodes but such attempts may suffer serious degradation under dynamic graph perturbations. In this paper, we generalize noisy supervision as a kind of self-supervised learning method and then propose a novel Bayesian self-supervision model, namely GraphSS, to address the issue. Extensive experiments demonstrate that GraphSS can not only affirmatively alert the perturbations on dynamic graphs but also effectively recover the prediction of a node classifier when the graph is under such perturbations. These two advantages prove to be generalized over three classic GCNs across five public graph datasets.

### Code

- [github](https://github.com/junzhuang-code/GraphSS?utm_source=catalyzex.com)

## [28 - Adversarial Training for Graph Neural Networks: Pitfalls, Solutions, and New Directions](https://arxiv.org/abs/2203.03762)

### Abstract

Despite its success in the image domain, adversarial training did not (yet) stand out as an effective defense for Graph Neural Networks (GNNs) against graph structure perturbations. In the pursuit of fixing adversarial training (1) we show and overcome fundamental theoretical as well as practical limitations of the adopted graph learning setting in prior work; (2) we reveal that more flexible GNNs based on learnable graph diffusion are able to adjust to adversarial perturbations, while the learned message passing scheme is naturally interpretable; (3) we introduce the first attack for structure perturbations that, while targeting multiple nodes at once, is capable of handling global (graph-level) as well as local (node-level) constraints. Including these contributions, we demonstrate that adversarial training is a state-of-the-art defense against adversarial structure perturbations.

### Code

- [github](https://www.cs.cit.tum.de/daml/adversarial-training/)

## [29 - Watermarking Graph Neural Networks based on Backdoor Attacks](https://arxiv.org/abs/2110.11024)

### Abstract

Graph Neural Networks (GNNs) have achieved promising performance in various real-world applications. Building a powerful GNN model is not a trivial task, as it requires a large amount of training data, powerful computing resources, and human expertise in fine-tuning the model. Moreover, with the development of adversarial attacks, e.g., model stealing attacks, GNNs raise challenges to model authentication. To avoid copyright infringement on GNNs, verifying the ownership of the GNN models is necessary.
This paper presents a watermarking framework for GNNs for both graph and node classification tasks. We 1) design two strategies to generate watermarked data for the graph classification task and one for the node classification task, 2) embed the watermark into the host model through training to obtain the watermarked GNN model, and 3) verify the ownership of the suspicious model in a black-box setting. The experiments show that our framework can verify the ownership of GNN models with a very high probability (up to 99%) for both tasks. Finally, we experimentally show that our watermarking approach is robust against a state-of-the-art model extraction technique and four state-of-the-art defenses against backdoor attacks.

### Code

- [github](https://github.com/junzhuang-code/GraphSS?utm_source=catalyzex.com)

## [30 - Adversarial Embedding: A robust and elusive Steganography and Watermarking technique](https://arxiv.org/abs/1912.01487)

### Abstract

We propose adversarial embedding, a new steganography and watermarking technique that embeds secret information within images. The key idea of our method is to use deep neural networks for image classification and adversarial attacks to embed secret information within images. Thus, we use the attacks to embed an encoding of the message within images and the related deep neural network outputs to extract it. The key properties of adversarial attacks (invisible perturbations, nontransferability, resilience to tampering) offer guarantees regarding the confidentiality and the integrity of the hidden messages. We empirically evaluate adversarial embedding using more than 100 models and 1,000 messages. Our results confirm that our embedding passes unnoticed by both humans and steganalysis methods, while at the same time impedes illicit retrieval of the message (less than 13% recovery rate when the interceptor has some knowledge about our model), and is resilient to soft and (to some extent) aggressive image tampering (up to 100% recovery rate under jpeg compression). We further develop our method by proposing a new type of adversarial attack which improves the embedding density (amount of hidden information) of our method to up to 10 bits per pixel.

### Code

- [github](https://github.com/yamizi/Adversarial-Embedding)

## [31 - Watermarking Neural Networks With Watermarked Images](https://ieeexplore.ieee.org/document/9222304)

### Abstract

Watermarking neural networks is a quite important means to protect the intellectual property (IP) of neural networks. In this paper, we introduce a novel digital watermarking framework suitable for deep neural networks that output images as the results, in which any image outputted from a watermarked neural network must contain a certain watermark. Here, the host neural network to be protected and a watermark-extraction network are trained together, so that, by optimizing a combined loss function, the trained neural network can accomplish the original task while embedding a watermark into the outputted images. This work is totally different from previous schemes carrying a watermark by network weights or classification labels of the trigger set. By detecting watermarks in the outputted images, this technique can be adopted to identify the ownership of the host network and find whether an image is generated from a certain neural network or not. We demonstrate that this technique is effective and robust on a variety of image processing tasks, including image colorization, super-resolution, image editing, semantic segmentation and so on.

### Code

- [github]()

## [32 - DeepSigns: An End-to-End Watermarking Framework for Ownership Protection of Deep Neural Networks](https://www.researchgate.net/publication/332213758_DeepSigns_An_End-to-End_Watermarking_Framework_for_Ownership_Protection_of_Deep_Neural_Networks)

### Abstract

Deep Learning (DL) models have created a paradigm shift in our ability to comprehend raw data in various important fields, ranging from intelligence warfare and healthcare to autonomous transportation and automated manufacturing. A practical concern, in the rush to adopt DL models as a service, is protecting the models against Intellectual Property (IP) infringement. DL models are commonly built by allocating substantial computational resources that process vast amounts of proprietary training data. The resulting models are therefore considered to be an IP of the model builder and need to be protected to preserve the owner's competitive advantage. We propose DeepSigns, the first end-to-end IP protection framework that enables developers to systematically insert digital watermarks in the target DL model before distributing the model. DeepSigns is encapsulated as a high-level wrapper that can be leveraged within common deep learning frameworks including TensorFlow and PyTorch. The libraries in DeepSigns work by dynamically learning the Probability Density Function (pdf) of activation maps obtained in different layers of a DL model. DeepSigns uses the low probabilistic regions within the model to gradually embed the owner's signature (watermark) during DL training while minimally affecting the overall accuracy and training overhead. DeepSigns can demonstrably withstand various removal and transformation attacks, including model pruning, model fine-tuning, and watermark overwriting. We evaluate DeepSigns performance on a wide variety of DL architectures including wide residual convolution neural networks, multi-layer perceptrons, and long short-term memory models. Our extensive evaluations corroborate DeepSigns' effectiveness and applicability. We further provide a highly-optimized accompanying API to facilitate training watermarked neural networks with a training overhead as low as 2.2%.

### Code

- [github]()

## [33 - Robust Graph Data Learning via Latent Graph Convolutional Representation](https://arxiv.org/abs/1904.11883)

### Abstract

Graph Convolutional Representation (GCR) has achieved impressive performance for graph data representation. However, existing GCR is generally defined on the input fixed graph which may restrict the representation capacity and also be vulnerable to the structural attacks and noises. To address this issue, we propose a novel Latent Graph Convolutional Representation (LatGCR) for robust graph data representation and learning. Our LatGCR is derived based on reformulating graph convolutional representation from the aspect of graph neighborhood reconstruction. Given an input graph A, LatGCR aims to generate a flexible latent graph A˜ for graph convolutional representation which obviously enhances the representation capacity and also performs robustly w.r.t graph structural attacks and noises. Moreover, LatGCR is implemented in a self-supervised manner and thus provides a basic block for both supervised and unsupervised graph learning tasks. Experiments on several datasets demonstrate the effectiveness and robustness of LatGCR.

### Code

- [github]()

## [34 - Topology Attack and Defense for Graph Neural Networks: An Optimization Perspective](https://arxiv.org/abs/1906.04214)

### Abstract

Graph neural networks (GNNs) which apply the deep neural networks to graph data have achieved significant performance for the task of semi-supervised node classification. However, only few work has addressed the adversarial robustness of GNNs. In this paper, we first present a novel gradient-based attack method that facilitates the difficulty of tackling discrete graph data. When comparing to current adversarial attacks on GNNs, the results show that by only perturbing a small number of edge perturbations, including addition and deletion, our optimization-based attack can lead to a noticeable decrease in classification performance. Moreover, leveraging our gradient-based attack, we propose the first optimization-based adversarial training for GNNs. Our method yields higher robustness against both different gradient based and greedy attack methods without sacrificing classification accuracy on original graph.

### Code

- [github](https://github.com/KaidiXu/GCN_ADV_Train)

## [35 - Investigating Robustness and Interpretability of Link Prediction via Adversarial Modifications](https://arxiv.org/abs/1905.00563)

### Abstract

Representing entities and relations in an embedding space is a well-studied approach for machine learning on relational data. Existing approaches, however, primarily focus on improving accuracy and overlook other aspects such as robustness and interpretability. In this paper, we propose adversarial modifications for link prediction models: identifying the fact to add into or remove from the knowledge graph that changes the prediction for a target fact after the model is retrained. Using these single modifications of the graph, we identify the most influential fact for a predicted link and evaluate the sensitivity of the model to the addition of fake facts. We introduce an efficient approach to estimate the effect of such modifications by approximating the change in the embeddings when the knowledge graph changes. To avoid the combinatorial search over all possible facts, we train a network to decode embeddings to their corresponding graph components, allowing the use of gradient-based optimization to identify the adversarial modification. We use these techniques to evaluate the robustness of link prediction models (by measuring sensitivity to additional facts), study interpretability through the facts most responsible for predictions (by identifying the most influential neighbors), and detect incorrect facts in the knowledge base.

### Code

- [github](https://github.com/pouyapez/criage)

## [36 - Robust Graph Convolutional Networks Against Adversarial Attacks](http://pengcui.thumedialab.com/papers/RGCN.pdf)

### Abstract

Graph Convolutional Networks (GCNs) are an emerging type of neural network model on graphs which have achieved state-ofthe-art performance in the task of node classification. However, recent studies show that GCNs are vulnerable to adversarial attacks, i.e. small deliberate perturbations in graph structures and node attributes, which poses great challenges for applying GCNs to real world applications. How to enhance the robustness of GCNs remains a critical open problem. To address this problem, we propose Robust GCN (RGCN), a novel model that “fortifies” GCNs against adversarial attacks. Specifically, instead of representing nodes as vectors, our method adopts Gaussian distributions as the hidden representations of nodes in each convolutional layer. In this way, when the graph is attacked, our model can automatically absorb the effects of adversarial changes in the variances of the Gaussian distributions. Moreover, to remedy the propagation of adversarial attacks in GCNs, we propose a variance-based attention mechanism, i.e. assigning different weights to node neighborhoods according to their variances when performing convolutions. Extensive experimental results demonstrate that our proposed method can effectively improve the robustness of GCNs. On three benchmark graphs, our RGCN consistently shows a substantial gain in node classification accuracy compared with state-of-the-art GCNs against various adversarial attack strategies.

### Code

- [github](https://github.com/pouyapez/criage)

## [37 - Virtual Adversarial Training on Graph Convolutional Networks in Node Classification](https://arxiv.org/abs/1902.11045)

### Abstract

### Code

- [github](https://github.com/thumanlab/nrlweb/blob/master/static/assets/download/RGCN.zip)

## [38 - Latent Adversarial Training of Graph Convolution Networks](https://graphreason.github.io/papers/35.pdf)

### Abstract

Despite the recent success of graph convolution
networks (GCNs) in modeling graph structured
data, its vulnerability to adversarial attacks have
been revealed and attacks on both node feature
and graph structure have been designed. Direct
extension of adversarial sample based defense
algorithms meets with immediate challenge because computing the adversarial network requires
substantial cost. We propose addressing this issue
by perturbing the latent representations in GCNs,
which not only dispenses with adversarial network
generation, but also attains improved robustness
and accuracy by respecting the latent manifold of
the data. Experimental results confirm the superior performance over strong baselines.

### Code

- [github](https://github.com/cshjin/LATGCN)

## [39 - Batch Virtual Adversarial Training for Graph Convolutional Networks](https://arxiv.org/abs/1902.09192)

### Abstract

We present batch virtual adversarial training (BVAT), a novel regularization method for graph convolutional networks (GCNs). BVAT addresses the shortcoming of GCNs that do not consider the smoothness of the model's output distribution against local perturbations around the input. We propose two algorithms, sample-based BVAT and optimization-based BVAT, which are suitable to promote the smoothness of the model for graph-structured data by either finding virtual adversarial perturbations for a subset of nodes far from each other or generating virtual adversarial perturbations for all nodes with an optimization process. Extensive experiments on three citation network datasets Cora, Citeseer and Pubmed and a knowledge graph dataset Nell validate the effectiveness of the proposed method, which establishes state-of-the-art results in the semi-supervised node classification tasks.

### Code

- [github]()

## [40 - Adversarial Robustness of Similarity-Based Link Prediction](https://arxiv.org/abs/1909.01432)

### Abstract

Link prediction is one of the fundamental problems in social network analysis. A common set of techniques for link prediction rely on similarity metrics which use the topology of the observed subnetwork to quantify the likelihood of unobserved links. Recently, similarity metrics for link prediction have been shown to be vulnerable to attacks whereby observations about the network are adversarially modified to hide target links. We propose a novel approach for increasing robustness of similarity-based link prediction by endowing the analyst with a restricted set of reliable queries which accurately measure the existence of queried links. The analyst aims to robustly predict a collection of possible links by optimally allocating the reliable queries. We formalize the analyst problem as a Bayesian Stackelberg game in which they first choose the reliable queries, followed by an adversary who deletes a subset of links among the remaining (unreliable) queries by the analyst. The analyst in our model is uncertain about the particular target link the adversary attempts to hide, whereas the adversary has full information about the analyst and the network. Focusing on similarity metrics using only local information, we show that the problem is NP-Hard for both players, and devise two principled and efficient approaches for solving it approximately. Extensive experiments with real and synthetic networks demonstrate the effectiveness of our approach.

### Code

- [github]()

## [41 - Adversarial Training Methods for Network Embedding](https://arxiv.org/abs/1908.11514)

### Abstract

Network Embedding is the task of learning continuous node representations for networks, which has been shown effective in a variety of tasks such as link prediction and node classification. Most of existing works aim to preserve different network structures and properties in low-dimensional embedding vectors, while neglecting the existence of noisy information in many real-world networks and the overfitting issue in the embedding learning process. Most recently, generative adversarial networks (GANs) based regularization methods are exploited to regularize embedding learning process, which can encourage a global smoothness of embedding vectors. These methods have very complicated architecture and suffer from the well-recognized non-convergence problem of GANs. In this paper, we aim to introduce a more succinct and effective local regularization method, namely adversarial training, to network embedding so as to achieve model robustness and better generalization performance. Firstly, the adversarial training method is applied by defining adversarial perturbations in the embedding space with an adaptive L2 norm constraint that depends on the connectivity pattern of node pairs. Though effective as a regularizer, it suffers from the interpretability issue which may hinder its application in certain real-world scenarios. To improve this strategy, we further propose an interpretable adversarial training method by enforcing the reconstruction of the adversarial examples in the discrete graph domain. These two regularization methods can be applied to many existing embedding models, and we take DeepWalk as the base model for illustration in the paper. Empirical evaluations in both link prediction and node classification demonstrate the effectiveness of the proposed methods.

### Code

- [github](https://github.com/wonniu/AdvT4NE_WWW2019)

## [42 - Graph Interpolating Activation Improves Both Natural and Robust Accuracies in Data-Efficient Deep Learning](https://arxiv.org/abs/1907.06800)

### Abstract

Improving the accuracy and robustness of deep neural nets (DNNs) and adapting them to small training data are primary tasks in deep learning research. In this paper, we replace the output activation function of DNNs, typically the data-agnostic softmax function, with a graph Laplacian-based high dimensional interpolating function which, in the continuum limit, converges to the solution of a Laplace-Beltrami equation on a high dimensional manifold. Furthermore, we propose end-to-end training and testing algorithms for this new architecture. The proposed DNN with graph interpolating activation integrates the advantages of both deep learning and manifold learning. Compared to the conventional DNNs with the softmax function as output activation, the new framework demonstrates the following major advantages: First, it is better applicable to data-efficient learning in which we train high capacity DNNs without using a large number of training data. Second, it remarkably improves both natural accuracy on the clean images and robust accuracy on the adversarial images crafted by both white-box and black-box adversarial attacks. Third, it is a natural choice for semi-supervised learning. For reproducibility, the code is available at \url{this https URL}.

### Code

- [github](https://github.com/BaoWangMath/DNN-DataDependentActivation)

## [43 - Bayesian graph convolutional neural networks for semi-supervised classification](https://arxiv.org/abs/1811.11103)

### Abstract

Recently, techniques for applying convolutional neural networks to graph-structured data have emerged. Graph convolutional neural networks (GCNNs) have been used to address node and graph classification and matrix completion. Although the performance has been impressive, the current implementations have limited capability to incorporate uncertainty in the graph structure. Almost all GCNNs process a graph as though it is a ground-truth depiction of the relationship between nodes, but often the graphs employed in applications are themselves derived from noisy data or modelling assumptions. Spurious edges may be included; other edges may be missing between nodes that have very strong relationships. In this paper we adopt a Bayesian approach, viewing the observed graph as a realization from a parametric family of random graphs. We then target inference of the joint posterior of the random graph parameters and the node (or graph) labels. We present the Bayesian GCNN framework and develop an iterative learning procedure for the case of assortative mixed-membership stochastic block models. We present the results of experiments that demonstrate that the Bayesian formulation can provide better performance when there are very few labels available during the training process.

### Code

- [github](https://github.com/huawei-noah/BGCN)

## [44 - Graph Adversarial Training: Dynamically Regularizing Based on Graph Structure](https://arxiv.org/abs/1902.08226)

### Abstract

Recent efforts show that neural networks are vulnerable to small but intentional perturbations on input features in visual classification tasks. Due to the additional consideration of connections between examples (\eg articles with citation link tend to be in the same class), graph neural networks could be more sensitive to the perturbations, since the perturbations from connected examples exacerbate the impact on a target example. Adversarial Training (AT), a dynamic regularization technique, can resist the worst-case perturbations on input features and is a promising choice to improve model robustness and generalization. However, existing AT methods focus on standard classification, being less effective when training models on graph since it does not model the impact from connected examples.
In this work, we explore adversarial training on graph, aiming to improve the robustness and generalization of models learned on graph. We propose Graph Adversarial Training (GraphAT), which takes the impact from connected examples into account when learning to construct and resist perturbations. We give a general formulation of GraphAT, which can be seen as a dynamic regularization scheme based on the graph structure. To demonstrate the utility of GraphAT, we employ it on a state-of-the-art graph neural network model --- Graph Convolutional Network (GCN). We conduct experiments on two citation graphs (Citeseer and Cora) and a knowledge graph (NELL), verifying the effectiveness of GraphAT which outperforms normal training on GCN by 4.51% in node classification accuracy. Codes are available via: this https URL.

### Code

- [github](https://github.com/fulifeng/GraphAT)

## [45 - Graph-Revised Convolutional Network](https://arxiv.org/abs/1911.07123)

### Abstract

Graph Convolutional Networks (GCNs) have received increasing attention in the machine learning community for effectively leveraging both the content features of nodes and the linkage patterns across graphs in various applications. As real-world graphs are often incomplete and noisy, treating them as ground-truth information, which is a common practice in most GCNs, unavoidably leads to sub-optimal solutions. Existing efforts for addressing this problem either involve an over-parameterized model which is difficult to scale, or simply re-weight observed edges without dealing with the missing-edge issue. This paper proposes a novel framework called Graph-Revised Convolutional Network (GRCN), which avoids both extremes. Specifically, a GCN-based graph revision module is introduced for predicting missing edges and revising edge weights w.r.t. downstream tasks via joint optimization. A theoretical analysis reveals the connection between GRCN and previous work on multigraph belief propagation. Experiments on six benchmark datasets show that GRCN consistently outperforms strong baseline methods by a large margin, especially when the original graphs are severely incomplete or the labeled instances for model training are highly sparse.

### Code

- [github](https://github.com/Maysir/GRCN)

## [46 - DefenseVGAE: Defending against Adversarial Attacks on Graph Data via a Variational Graph Autoencoder](https://arxiv.org/abs/2006.08900)

### Abstract

Graph neural networks (GNNs) achieve remarkable performance for tasks on graph data. However, recent works show they are extremely vulnerable to adversarial structural perturbations, making their outcomes unreliable. In this paper, we propose DefenseVGAE, a novel framework leveraging variational graph autoencoders(VGAEs) to defend GNNs against such attacks. DefenseVGAE is trained to reconstruct graph structure. The reconstructed adjacency matrix can reduce the effects of adversarial perturbations and boost the performance of GCNs when facing adversarial attacks. Our experiments on a number of datasets show the effectiveness of the proposed method under various threat models. Under some settings it outperforms existing defense strategies. Our code has been made publicly available at this https URL.

### Code

- [github](https://github.com/zhangao520/defense-vgae)

## [47 - Enhancing Graph Neural Network-based Fraud Detectors against Camouflaged Fraudsters](https://arxiv.org/abs/2008.08692)

### Abstract

Graph Neural Networks (GNNs) have been widely applied to fraud detection problems in recent years, revealing the suspiciousness of nodes by aggregating their neighborhood information via different relations. However, few prior works have noticed the camouflage behavior of fraudsters, which could hamper the performance of GNN-based fraud detectors during the aggregation process. In this paper, we introduce two types of camouflages based on recent empirical studies, i.e., the feature camouflage and the relation camouflage. Existing GNNs have not addressed these two camouflages, which results in their poor performance in fraud detection problems. Alternatively, we propose a new model named CAmouflage-REsistant GNN (CARE-GNN), to enhance the GNN aggregation process with three unique modules against camouflages. Concretely, we first devise a label-aware similarity measure to find informative neighboring nodes. Then, we leverage reinforcement learning (RL) to find the optimal amounts of neighbors to be selected. Finally, the selected neighbors across different relations are aggregated together. Comprehensive experiments on two real-world fraud datasets demonstrate the effectiveness of the RL algorithm. The proposed CARE-GNN also outperforms state-of-the-art GNNs and GNN-based fraud detectors. We integrate all GNN-based fraud detectors as an opensource toolbox: this https URL. The CARE-GNN code and datasets are available at this https URL.

### Code

- [github](https://github.com/safe-graph/DGFraud)

## [48 - On the Robustness of Cascade Diffusion under Node Attacks](https://www.cs.au.dk/~karras/robustIC.pdf)

### Abstract

How can we assess a network’s ability to maintain its functionality
under attacks? Network robustness has been studied extensively
in the case of deterministic networks. However, applications such
as online information diffusion and the behavior of networked
public raise a question of robustness in probabilistic networks. We
propose three novel robustness measures for networks hosting a
diffusion under the Independent Cascade (IC) model, susceptible
to node attacks. The outcome of such a process depends on the
selection of its initiators, or seeds, by the seeder, as well as on two
factors outside the seeder’s discretion: the attack strategy and the
probabilistic diffusion outcome. We consider three levels of seeder
awareness regarding these two uncontrolled factors, and evaluate
the network’s viability aggregated over all possible extents of node
attacks. We introduce novel algorithms from building blocks found
in previous works to evaluate the proposed measures. A thorough
experimental study with synthetic and real, scale-free and homogeneous networks establishes that these algorithms are effective and
efficient, while the proposed measures highlight differences among
networks in terms of robustness and the surprise they furnish when
attacked. Last, we devise a new measure of diffusion entropy that
can inform the design of probabilistically robust networks.

### Code

- [github](https://github.com/allogn/robustness)

## [49 - On The Stability of Polynomial Spectral Graph Filters](https://ieeexplore.ieee.org/abstract/document/9054072)

### Abstract

Spectral graph filters are a key component in state-of-the-art machine learning models used for graph-based learning, such as graph neural networks. For certain tasks stability of the spectral graph filters is important for learning suitable representations. Understanding the type of structural perturbation to which spectral graph filters are robust lets us reason as to when we may expect them to be well suited to a learning task. In this work, we first prove that polynomial graph filters are stable with respect to the change in the normalised graph Laplacian matrix. We then show empirically that properties of a structural perturbation, specifically the relative locality of the edges removed in a binary graph, effect the change in the normalised graph Laplacian. Together, our results have implications on designing robust graph filters and representations under structural perturbation.

### Code

- [github](https://github.com/henrykenlay/spgf)

## [50 - Graph Structure Learning for Robust Graph Neural Networks](https://arxiv.org/abs/2005.10203)

### Abstract

Graph Neural Networks (GNNs) are powerful tools in representation learning for graphs. However, recent studies show that GNNs are vulnerable to carefully-crafted perturbations, called adversarial attacks. Adversarial attacks can easily fool GNNs in making predictions for downstream tasks. The vulnerability to adversarial attacks has raised increasing concerns for applying GNNs in safety-critical applications. Therefore, developing robust algorithms to defend adversarial attacks is of great significance. A natural idea to defend adversarial attacks is to clean the perturbed graph. It is evident that real-world graphs share some intrinsic properties. For example, many real-world graphs are low-rank and sparse, and the features of two adjacent nodes tend to be similar. In fact, we find that adversarial attacks are likely to violate these graph properties. Therefore, in this paper, we explore these properties to defend adversarial attacks on graphs. In particular, we propose a general framework Pro-GNN, which can jointly learn a structural graph and a robust graph neural network model from the perturbed graph guided by these properties. Extensive experiments on real-world graphs demonstrate that the proposed framework achieves significantly better performance compared with the state-of-the-art defense methods, even when the graph is heavily perturbed. We release the implementation of Pro-GNN to our DeepRobust repository for adversarial attacks and defenses (footnote: this https URL). The specific experimental settings to reproduce our results can be found in this https URL.

### Code

- [github-1](https://github.com/DSE-MSU/DeepRobust)
- [github-2](https://github.com/ChandlerBang/Pro-GNN)
