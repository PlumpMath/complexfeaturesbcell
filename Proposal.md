# Complex Features in Prediction of Discontinuous B-cell Epitopes

Kyle I S Harrington<sup>1,*</sup>, James Chin <sup>2</sup>

<sup>1</sup> Brandeis, Tufts, Harvard Med.

<sup>2</sup> Brandeis, Dartmouth.

<sup>*</sup> Corresponding author: kyleh@cs.brandeis.edu

## Introduction

To date, most efforts to predict B-cell epitopes have been based upon linear
sequence data, which precludes many structures with intertwined surfaces. Existing
work on the prediction of discontinuous B-cell epitopes has revealed a number of
computable features that help predict epitope binding affinity. We extend this
research by discovering complex high-level features-based based upon physical
characteristics.

B-cell epitopes are regions of molecules recognized by antibodies of the immune system. Characterization of B-cell epitopes is a crucial step for understanding the immunological basis of bio-recognition. Knowledge of the locations of B-cell epitopes can aid the development of peptide vaccines or used to induce the production of antibodies for diagnostic and therapeutic applications.

<!-- %The ability of an antibody to specifically bind an antigen forms the basis of numerous immunodetection and immunotherapeutics applications.
Hence, it is of interest to develop improved methods for predicting B-cell epitopes.\\ -->

<!-- % Defining the problem:
Although it has been estimated that over 90% of B-cell epitopes are
discontinuous (i.e.,segments separated in antigen protein sequence and brought
into proximity by protein folding) \cite{Barlow1986}, most existing methods for
prediction of B-cell epitopes are designed to predict linear amino acid
sequences (continuous epitopes) using exclusively use protein sequences as
input. \cite{Hopp1983, Odorico2003} -->


## B-cell Epitope Classification

<!-- %Most existing methods do a poor job of predicting discontinuous epitopes.
% How good is current continuous epitope prediction models on predicting linear epitopes? -->
Existing methods to predict the location of continuous epitopes and patterns in proteins are based on the reported correlation between physicochemical properties of amino acids and the locations of linear B-cell epitopes within protein sequences . Physicochemical properties such as hydrophilicity, flexibility, turns or solvent accessibility were used in BEPITOPE (Odorico and Pellequer, 2003). Based a recent exhaustive assessment of 484 amino acid propensity scales that combined a range of profile parameters by (Blythe and Flower, 2005),  the B-cell epitope prediction based on amino acid sequence information performed only marginally better than random (Manzalawy et al, 2008).

<!-- Machine learning approaches have been used to improve the accuracy of linear B-cell epitope prediction methods. Bepipred (Larsen et al, 2006) uses two amino acid propensity scales and a Hidden Markov Model (HMM) trained on linear epitopes to yield a slight improvement in prediction accuracy relative to techniques that rely solely on analysis of amino acid physicochemical properties. ABCPred uses artificial neural networks for predicting linear B-cell epitopes had a best performance of 66\% accuracy when evaluated on a non-redundant data set of 700 B-cell epitopes and 700 non-epitope peptides, using fivefold crow-validation tests and input sequence windows ranging from 10 to 20 amino acids. BCPred, a method for predicting linear B-cell epitopes using an SVM machine learning method reported outperforming 11 SVM-based classifiers with an AUC of 0.758 (Manzalawy, 2008). -->

<!-- Although most B-cell epitopes are discontinous, a limited number of prediction methods exist for discontinuous epitope prediction exist. The existing methods include CEP (Kulkarni-Kale et al, 2005) , Discotope (Andersen et al, 2006), PEPITO (Sweredoski et al, 2008), ElliPro (Ponomarenko et al, 2008), SEPPA (Sun et al, 2009), EPITOPIA (Rubinstein et al, 2009a; 2009b) and EPCES (Liang et al, 2009). These methods to predict discontinuous epitopes have had limited success in predicting discontinuous success.
EPSVR and EPMeta are server applications for discontinuous epitope prediction that use Support Vector Regression (SVR) to integrate multiple attributes for discontinuous epitope prediction, reported an AUC higher than that of any other existing single server (Liang et al, 2010). EPSVR has a reported AUC of 0.597, and EPMeta has a reported AUC of 0.638, which is significantly higher than PEPITO and Discotope ($p-value <$ 0.05) (Liang et al, 2010). -->

### Data

A list of experimentally determined protein antigen-antibody structures and corresponding
epitope binding information was
obtained from IEDB (Vita et al, 2010). The
list was filtered to contain only structures determined to a resolution less
than 3 Angstrom with protein antigens of greater than 25 amino acids. Coordinate
files corresponding to the filtered list were downloaded from the Protein Data
Bank (PDB, http://www.rcsb.org/pdb). We estimate that the final data set will
contain around 100 antibody-antigen pairs. Epitope residues in the data set were
defined as antigen amino acids having atoms within 4 Angstroms of antibody atoms.

### Basis features
We compute a set of features based upon the crystal structures obtained from
RCSB PDB database: number of neighbors, central residue and patch side chain pKa, central residue and patch hydrophilicity, ratio of amino acid composition, and half sphere exposure. Features are computed with BioJava (Prlic et al, 2012) and the corresponding code is available as open-source (see Github).

## Complex Features

We extend the intuition from support vector machines (SVMs) which involves mapping to a higher dimensional space where linear separability may be more easily achieved. We introduce these as complex features which are functions expressed using a set of basis features, mathematical operators (i.e. logical, arithmetic, trigonometric operations), and conditional expressions.
Complex features are encoded in the Push programming language
(Spector et al, 2005). Push is an expressive stack-based programming language designed for
 program synthesis. Complex features are constructed by randomly generating programs with the proposed bases.

## Experiments

Wrapper methods for feature selection (both forward selection and backward elimination) are applied to datasets constructed from basis features and complex features. Stratified cross-validation is used to construct 10-fold training/testing datasets because of the small number of epitope binding sites to non-binding sites. The improvement is calculated as a p-value using a 2-tailed t-test and the AUC ROC value.

### References

1. Odorico, M. and Pellequer, J.L., 2003. BEPITOPE: predicting the location of continuous epitopes and patterns in proteins. Journal of Molecular Recognition, 16(1), pp.20-22.

2. EL‐Manzalawy, Y., Dobbs, D. and Honavar, V., 2008. Predicting linear B‐cell epitopes using string kernels. Journal of molecular recognition, 21(4), pp.243-255.

3. Vita, R., Zarebski, L., Greenbaum, J.A., Emami, H., Hoof, I., Salimi, N., Damle, R., Sette, A. and Peters, B., 2010. The immune epitope database 2.0. Nucleic acids research, 38(suppl 1), pp.D854-D862.

4. Prlić, A., Yates, A., Bliven, S.E., Rose, P.W., Jacobsen, J., Troshin, P.V., Chapman, M., Gao, J., Koh, C.H., Foisy, S. and Holland, R., 2012. BioJava: an open-source framework for bioinformatics in 2012. Bioinformatics, 28(20), pp.2693-2695.

5. Spector, L., Klein, J. and Keijzer, M., 2005, June. The push3 execution stack and the evolution of control. In Proceedings of the 7th annual conference on Genetic and evolutionary computation (pp. 1689-1696). ACM.
