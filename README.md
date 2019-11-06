# GRN and Gene_Expression_Analysis
GRN is a collection of **molecular regulators** that interact with `each other` and with `other substances` in the cell to govern the gene expression levels of mRNA and proteins. These play a central role in morphogenesis, the creation of body structures. The regulator can be DNA, RNA, protein and complexes of these. The interaction can be direct or indirect. GRN model can be considered as a matrix(T_iXj) of positive, negative or zero connections by which one transcription factor can enhance or repress another.
 - The regulation is enhancing if the entry is positive and repressing if it is negative. A zero entry signifies no connection between gene product j and gene i. 
 - enzymes(catalyst) allows biochemical reaction to occur in our body like a researcher in the lab...like a lock that is open when a specific molecule works as a key.  
   - transcription process: DNA -> mRNA 
   - translation process: mRNA -> protein ... so manufacture human, fish,...

#### We want to derive full GRN involving regulatory elements and identify `connections and interactions` between genes:  
 - that fit the gene expression profile data and 
 - that can lead to the subsequent analysis of regulatory and transcription factors that help in the construction of GRN model matrix.

Once knowing what kind of genes are expressed in what pattern, we can  ???

> Background?
 - __Reverse engineering of GRNs?__ 
   - In each type of cell, different genes are expressed (turned on) or silenced (turned off). By identifying which genes in the sick cells are working abnormally, doctors can better diagnose the ailment. One way they do this is to use a **DNA microarray** to determine the expression levels of genes. When a gene is expressed, a certain protein is produced. When a gene is expressed in a cell, it generates `messenger RNA` (mRNA). `**Overexpressed genes** generate more mRNA. This can be detected on the **microarray**`.
   - **Technologies** measuring **gene expression levels**(gene turned on) has created a database for inferring GRNs. However, the nature of these data has made this GRN inferring process very difficult and the large scale quantitative analysis on real biological datasets cannot be performed, to date, as existing approaches are not suitable for **real microarray data** which are noisy and insufficient.

 - __GRN Model__
   - Mathematical models should be developed to capture the behavior of the system being modeled, and in some cases generate predictions corresponding with experimental observations.
   - The level of `mRNA concentrations` can be viewed as a snapshot of the genes expression levels **under certain conditions**. With a large enough set of snapshots, it should be theoretically possible to uncover the underlying gene regulatory network(GRN). 
   - **Modeling:** We can find parameters of the GRN model from available data. Once built, these GRN models can be used to predict the behaviour of the organism **under certain conditions**, related to different treatments or diseases(predict its behaviour under different conditions).
     - `genes` are viewed as **variables** that change their (expression) values in time.
       - Depending on the type of variables used, methods can be classiﬁed as discrete or continuous, deterministic or stochastic, or as hybrid methods
     - two typical approaches:
       - 1) coarse-grained model
         - less detail on interations b/w genes
         - typically rely on **discrete variables**
         - ex) Boolean networks, Bayesian networks, Petri Nets, rule sets, etc.
       - 2) fine-grained model
         - large network, complicated interactions b/w genes, an enormous number of parameters. 
         - typically based on **continuous variables**
         - ex) S-Systems(Systems of Differential Equations), ANN, thermodynamic models, Hybrid Petri Nets, or analysing only subnetworks of the entire GRN, etc.
       - Both inference and analysis of them are difficult, thus global(high-level) analysis of the network has its attractions.
         - Combining levels of detail in a top-down or bottom-up approach..moving from the `coarse` to the `fine` or vice versa...

 - __GRN fitting Method and inference__ 
 Two different approaches for GRN model parameter inference are advocated in the literature: 1)finding relations for the entire network or 2)analysing a single gene at-a-time
   - Why Genetic Algorithm as an optimization method?
     - these are known to cope well with a large solution space!
     - it can be applied to both synthetic and real "gene expression" data from DNA microarrays.
     - when only limited data are available, it leads to **under-specfication of the system**`(i.e. the limited number of data points combined with the large number of parameters)`**. Under these circumstances, **EA**s become a good alternative to other fitting methods as they provide an efficient way of spanning the promising areas of the solution space!
     - in general, and in particular EA approaches have the benefit of flexibility in terms of adding **prior information** to the optimisation process.
       - This can be done at several stages, such as initialisation, fitness evaluation, mutation or crossover, etc.
       - An example of integrating biological knowledge in the algorithms implemented is using the sparsity of the GRN
       - previously known interactions could be introduced during initialisation, and during fitness evaluation (edges connecting genes with binding affinities could add to the fitness of the individual). 
   - Checkpoint(A): Scalability?
     - how it works based on...all the genes or the subset of them in the network????
     - quantitative behaviour:
       - ability to reproduce data? (indentifying the most important interactions ?)
       - parameter quality by size?
   
   - Checkpoint(B): Robustness to noise? 
     - With the presence of noise, show best balance for sensitivity-specificity ?
     - With the presence of noise, show best qualitative behaviour ?
  
  
## How to elucidate the `regulatory connections` and `interactions` between genes, proteins and other gene products ?
NN~; Can we determine **gene interactions** in temporal gene expression data using **genetic algorithms** combined with a **neural network component**? 

Classification method can be modified for use as a tool for determining the interactions between genes over time??

## DNA arrays
are capable of capturing the expression level of genes at one particular timepoint and, while they have been criticized for a variety of reasons (e.g., noise in measurement and, more importantly, lack of knowledge of how much mRNA actually makes it through to translation), they currently represent the best opportunity for scientists to examine the qualitative and quantitative expression of most genes in the human genome. 
 - All our genes together are known as our "genome." It completes mapping and understanding of all the genes of human beings.
 - The resulting data generated by DNA arrays, however, has proven somewhat of a challenge for traditional analytical techniques due largely to the **size** of the arrays themselves and the inherent **combinatorial problems**. 
 - `DNA array profile experiments` fall into two categories: 
   - 1)classification based approach
     - compare! ok?
     - data is obtained by **sampling just once** "a number of individual organisms or tissue samples" which differ in some respect from each other. Individuals are sampled and separated into classes according to either an **independent diagnosis** using traditional methods or a **class** being determined by the pathology of the individuals involved. It has a purpose to differentiate between those individuals diagnosed with the ailment and those without, **based solely on the gene expression values** of each of those individuals at one time-point. 
     
   - 2)temporal based approach
     - simulate! ok? Find the cause and effect! 
     - data is created by **measuring** gene expression values **over a number of timesteps**, often while subjecting the organism to some stimulus, so that the **behavior of genes** in response to "certain experimental conditions" can be observed and measured to determine possible cause-effect relationships. 
     - The measurements gained from these studies often span thousands of genes (fields, attributes) and only a few timesteps (records), which makes it relatively unusual in structure and not as amenable to traditional analysis. 
     - Identify:  
       - **Direct Connection** with `excitatory(on)` and `inhibitory(off)` between **genes, gene products and proteins** if the time steps are close enough(a few seconds or minutes)
       - **Indirect Connections** if not (several minutes or hours). 
     
Two common difficulties in **Gene_Expression_Analysis**:
 - 1)"underdeterminism": Large features and Small records
 - 2)"curse of dimensionality": `Need of Combinations of gene` to correctly determine 
   - the **class of the sample** or 
   - the **activation of the regulated gene**. 
   - coz...**one single gene is unlikely to classify a sample or affect another gene**. In such circumstances, the search space grows to a much larger potential search space of **countless combinations**.

## Extracting GRN from temporal gene expression data 
How to deal with "curse of dimensionality" (large number of different models that display broadly the same behavior) caused mainly by "underdeterminism"..?
 - The majority of the methods make use of automated or human-derived methods for **determining functional groups of genes**(clustering) within the data. By using clustering, these approaches are able to discover hypothetical regulatory connections between groups of genes. And they also provide biologically plausible networks, provided that additional information about the organism is available. However, while the volume of additional information is increasing, there remain a large number of gene expression data sets for which this extra information is not available.
 - The neural-genetic approach mitigates underdeterminism in two significant ways:
   - 1) each gene has a restriction on the number of genes that can affect it in the network.
     - ex) the number of connections allowed between genes is limited to between one and five and between two and three on average
     - This restriction is in line with ideas developed from chaos theory, which proposed that the behavior of one gene is regulated by only a handful of other genes in the network.
   - 2) the approach can be repeated a number of times and only those genes that are present in a majority of the runs are allowed to be included in the final network. These restrictions are designed to allow the algorithm to discover robust connection networks.

## Extracting GRN from temporal gene expression data & ML
A number of methods have been used to generate GRN from (often artificial) data, including:Bayesian Networks, clustering, unsupervised neural networks, evolutionary algorithms, supervised learning algorithms.

a) Evolutionary approach using genetic algorithms(GAs) to extract GRN from gene expression data
 - __Weight Matrix Method:__
   - The chromosome of the GA is an encoded matrix of float values that correspond to the weight matrix between gene timesteps. Each individual, therefore, is a representation of the weight matrix.
   - The weight matrix is a set of connections from -1 to +1 that are summed and propagated through the sigmoid function to give the activation levels for each of the genes (which have previously been normalized).
   - The fitness function for the GA is calculated as the sum, over all timesteps, of the differences between the predicted and actual levels of activation for the gene expression.
   - The GA is then allowed to use its operators (crossover and mutation) to optimize this matrix of weights.
   - Another objective factored into the fitness function is that sparse matrices are required in this problem, to remove the possibility of all genes having an effect on all other genes. Therefore, a measure of the number of zero weights (signifying no effect) in the chromosome is used so that the fitness of individuals is partly based on the number of zeroes in the solution.
   
b) neural-genetic approach   
 - __RGANN (Repeated Genetic Algorithm with Neural Network):__ A single layer ANN + GA 
   - GA:
     - **one chromosome**(one individual) of the `GA` represents a small number of genes taken from the full set of genes. 
   - A single layer ANN: 
     - `ANN` is used to check how well the expression values of these genes(input to the ANN) at one timepoint affect another gene’s expression values(output from the ANN) at the subsequent timepoint, over a number of temporal datapoints. 
   - `GA` consists of a population of such chromosomes, and each chromosome is evaluated by the `ANN` for its effect on every gene in the database as part of one generation. 

By choosing appropriate GA mutation and crossover operators to alter the genes making up chromosomes, and by selecting “good” chromosomes(as determined by the ANN) at each generation, chromosomes in future generations should determine sets of genes that have the greatest effect in the data. 

So `ANN with RootMSE` is a fitness function used for selection! 

GA tries to determine the correct excitatory(gene_on) and inhibitory(gene_off) values that link genes in a network. In ANN, gradient descent determines the weights. This architecture is combined with a GA for generating hypothetical links where the connectivity is restricted to a maximum of N. Thus we can make use of the `connectivity restrictions imposed by the biology of the problem` as well as the sigmoid activation function for the `learning aspect` of the problem. 
<img src="https://user-images.githubusercontent.com/31917400/68314591-521a8280-00ae-11ea-8788-fccec157f761.jpg" />








































