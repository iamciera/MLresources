# Machine Learning to understand syntactic patterning of enhancers

This is a repository to keep track of all work that has been done in the purpose of understanding function in non-coding regions of the genome. 

## Predicting enhancers and regulatory regions <a name='genomics_enhancers'></a>

Here the inputs are typically “raw” DNA sequence, and convolutional networks (or layers) are often used to learn regularities within the sequence. 

**DanQ: a hybrid convolutional and recurrent deep neural network for quantifying the function of DNA sequences** [[github](https://github.com/uci-cbcl/DanQ)][[gitxiv](http://gitxiv.com/posts/aqrWwLoyg75jqNAYX/danq-a-hybrid-convolutional-and-recurrent-deep-neural)]

- **Purpose**: Made for predicting the function of non-protein coding DNA sequence. By Function, they mean predicting Protein binding and DNA accessibility (DNAse peaks and chip-seq peaks). 
- **How**: Uses a convolution layer to capture regulatory motifs (i e single DNA snippets that control the expression of genes, for instance), and a recurrent layer (of the LSTM type) to try to discover a “grammar” for how these single motifs work together (A layer for looking at the distance between motifs). 
- **Input/ Training Data**: Human [DeepSea](http://deepsea.princeton.edu/job/analysis/create/), 200 bp regions around TF binding Chip-Seq peaks. JASPAR for motifs.
- **Implemented on**: Based on Keras/Theano. Combines Convolution Neural Nets (motifs) and Recurrent Neural Nets (distance between motifs).

**Basset – learning the regulatory code of the accessible genome with deep convolutional neural networks** [[github](https://github.com/davek44/Basset)][[gitxiv](http://gitxiv.com/posts/fhET6G7gnBrGS8S9u/basset-learning-the-regulatory-code-of-the-accessible-genome)]

- **Purpose**: Predict cell-specific DNA accessibility and protein binding motifs for specific cell types.
- **How**: This package focuses on predicting the accessibility (or “openness”) of the chromatin – the physical packaging of the genetic information (DNA+associated proteins). This can exist in more condensed or relaxed states in different cell types, which is partly influenced by the DNA sequence (not completely, because then it would not differ from cell to cell.)
- **Input**:
- **Implemented with**: Based on [Torch](http://torch.ch/)

**DeepSEA – Predicting effects of noncoding variants with deep learning–based sequence model** [[web server](http://deepsea.princeton.edu/job/analysis/create/)][[paper](http://www.nature.com/nmeth/journal/v12/n10/full/nmeth.3547.html)]

*The method section in this paper is very clear*

- **Purpose**: Predict large-scale chromatin-profiling data, including TF binding, DNase I sensitivity and histone-mark profiles. Like the packages above, this one also models chromatin accessibility as well as the binding of certain proteins (transcription factors) to DNA and the presence of so-called histone marks that are associated with changes in accessibility. This piece of software seems to focus a bit more explicitly than the others on predicting how single-nucleotide mutations affect the chromatin structure.
- **How**: A deep convolutional network is a type of multilayer neural network. Integrating sequence information from a wide sequence context, learning sequence code at multiple spatial scales with a hierarchical architecture, and multitask joint learning of diverse chromatin factors sharing predictive features. 
-  **Input/ Training Data**: genome-wide chromatin profiles from the Encyclopedia of DNA Elements (ENCODE) and Roadmap Epigenomics projects. 690 TF binding profiles for 160 different TFs, 125 DHS profiles and 104 histone-mark profiles. Used conservation information ("evolutionary conservation") scores using PhastCons. 
- **Implemented with** - They made their own implementiation and have a web server, but all the code is hidden. Which sucks and is unuasable outside humans...or is it? 

**DeepBind – Predicting the sequence specificities of DNA- and RNA-binding proteins by deep learning** [[code](http://tools.genes.toronto.edu/deepbind/)][[paper](http://www.nature.com/nbt/journal/v33/n8/full/nbt.3300.html)]

*great intro on the challenges of predicting DNA and RNA binding. This is actually quite a nice tool over PWM for predicting TFBS.*

- **Purpose**: DeepBind focuses on predicting the binding specificities of DNA-binding or RNA-binding proteins, based on experiments such as ChIP-seq, ChIP-chip, RIP-seq,  protein-binding microarrays, and HT-SELEX. 
- **How**
- **Input/ Training data**: DeepBind uses a set of sequences and, for each sequence, an experimentally determined binding score.
- 

![](http://www.nature.com/nbt/journal/v33/n8/images_article/nbt.3300-F2.jpg)

**DeeperBind - Enhancing Prediction of Sequence Specificities of DNA Binding Proteins** [[preprint](https://arxiv.org/pdf/1611.05777.pdf)]

This is an attempt to improve on DeepBind by adding a recurrent sequence learning module (LSTM) after the convolutional layer(s). In this way, the authors propose to capture a positional dimension that is lost in the pooling step in the original DeepBind design. They claim that benchmarking shows that this architecture leads to superior performance compared to previous work.

**DeepMotif - Visualizing Genomic Sequence Classifications** [[paper](https://arxiv.org/abs/1605.01133)]

This is also about learning and predicting binding specificities of proteins to certain DNA patterns or "motifs". However, this paper makes use of a combination of convolutional layers and [highway networks](https://arxiv.org/pdf/1505.00387v2.pdf), with more layers than the DeepBind network. The authors also show how a learned classifier can generate typical DNA motifs by input optimization; applying back-propagation with all the weights held constant in order to find an input pattern that maximally activates the appropriate output node in the network.

**Convolutional Neural Network Architectures for Predicting DNA-Protein Binding** [[code](http://cnn.csail.mit.edu/)][[paper](http://bioinformatics.oxfordjournals.org/content/32/12/i121.full)]

This work describes a systematic exploration of convolutional neural network (CNN) architectures for DNA-protein binding. It concludes that the convolutional kernels are very important for the success of the networks on motif-based tasks. Interestingly, the authors have provided a Dockerized implementation of DeepBind from the Frey lab (see above) and also provide EC2-laucher scripts and code for comparing different GPU enabled models programmed in Caffe.

**PEDLA: predicting enhancers with a deep learning-based algorithmic framework** [[code](https://github.com/wenjiegroup/PEDLA)][[paper](http://biorxiv.org/content/early/2016/01/07/036129)]

This package is for predicting enhancers (stretches of DNA that can enhance the expression of a gene under certain conditions or in a certain kind of cell, often working at a distance from the gene itself) based on heterogeneous data from (e.g.) the ENCODE project, using 1,114 features altogether.

**DEEP: a general computational framework for predicting enhancers** [[paper](http://nar.oxfordjournals.org/content/early/2014/11/05/nar.gku1058.full)][[code](http://cbrc.kaust.edu.sa/deep/)]

An ensemble prediction method for enhancers.

**Genome-Wide Prediction of cis-Regulatory Regions Using Supervised Deep Learning Methods** (and several other papers applying various kinds of deep networks to regulatory region prediction) [[code](https://github.com/yifeng-li/DECRES)] (one [[paper](http://biorxiv.org/content/early/2016/02/28/041616)] out of several)

Wyeth Wasserman’s group have made a kind of [toolkit](https://github.com/yifeng-li/DECRES) (based on the Theano tutorials) for applying different kinds of deep learning architectures to cis-regulatory element (DNA stretches that can modulate the expression of a nearby gene) prediction. They use a specific “feature selection layer” in their nets to restrict the number of features in the models. This is implemented as an additional sparse one-to-one linear layer between the input layer and the first hidden layer of a multi-layer perceptron.

**FIDDLE: An integrative deep learning framework for functional genomic data inference** [[paper](http://biorxiv.org/content/early/2016/10/17/081380)][[code](https://github.com/ueser/FIDDLE)[[Youtube talk](https://www.youtube.com/watch?v=pcLTUsOm5pc&feature=youtu.be&list=PLlMMtlgw6qNjROoMNTBQjAcdx53kV50cS&t=2411)]

The group predicted transcription start site and regulatory regions but claims this solution could be easily generalized and predict other features too. FIDDLE stands for Flexible Integration of Data with Deep LEarning. The idea (nicely explained by the author in the YouTube video above) is to model several genomic signals jointly using convolutional networks. This could be for example DNase-seq, ATAC-seq, ChIP-seq, TSS-seq, maybe RNA-seq signals (as in .wig files with one value per base in the genome).
