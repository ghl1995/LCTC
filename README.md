# Linear Combinations of Template Conformations (LCTC): AnEfficient Method to Quantify Structural Distributions inHeterogeneous Cryo-EM Datasets

## 1.Introduction
Flexible  biomolecules  exist  in  an  ensemble  of  conformations  in  solution  that  havefunctional importance.  Cryo-EM can detect protein conformations frozen in solution andthus provide a promising way to characterize these conformational changes.  However, itremains challenging for existing software to elucidate multiple conformations and theirequilibrium distributions from a Cryo-EM dataset.  Analogous to the idea of constructingmolecular orbitals via the linear combination of atomic orbitals (“basis set”) to obtainthe  electronic  wave  functions,  we  developed  a  new  algorithm:  Linear  Combinations  ofTemplate Conformations (LCTC) to obtain multiple conformations and their populationsfrom Cryo-EM datasets.  Different from the widely used Clustering-based or MaximumLikelihood-based methods in Cryo-EM studies, LCTC assigns 2D images to the template3D structures (“basis set”) obtained by Multi-body Refinement of RELION via a noveltwo-stage matching algorithm.  The key advantage of our algorithm lies in an initial rapidassignment of experimental 2D images to template 2D images based on auto-correlationfunctions  of  image  contours.   This  first-stage  matching  process  can  efficiently  identifya  subset  of  experimental  2D  images  close  to  template  images  to  remove  the  majorityof irrelevant experimental 2D images.  This enables a subsequently accurate,  but moreexpensive pixel-pixel matching of images with a fewer number of experimental 2D images.

Our scheme is composed of four steps: 1) The best viewing angle to distinguish conformational changes was identified. 2) Template 3D structures generated by Multi-body Refinement of RELION were projected onto a number of viewing angles in proximity to the best viewing angle to generate template 2D images. 3) Cryo-EM 2D images were assigned to template 2D images via a two-stage matching process, in which the first computation of the pairwise distance was based on auto-correlation functions of the contours of masked images. Then comparison was performed on the pairwise distance based on pixel-pixel matching. 4) The populations of template structures were obtained.

## 2.Requirements
python, linux system and xmipp

## 3.Dataset
Each dataset is consisted of template structures and experimental structures. We use two expmples to test our algorithm, one is 
simulated dataset: Taq RNAP, the other is real dataset: Eco RNAP. 

We provided simualted dataset: open.vol, close.vol, intermediate.vol(same as test data and templates) 
and real dataset:6P1K.vol(test data), H_EV2_red.vol, H_EV2_grey.vol, H_EV2_blue.vol(templates), templates are generated by multi-body refinement of Relion.

## 4.RUN
Preprocess: you can use command: 
`xmipp_xmipp_volume_from_pdb -i open.pdb -o open.vol`     transfer pdb file to vol file

`xmipp_image_convert -i open.vol -o open.mrc`            transfer vol file to mrc file

run our algorithm: `python TSTM.py --datatype='sim' --vol_size=128`, the output is '2nd_stage_brute_force_classification_result.dat' 

and `python ./two_stage_matching/analyze_population.py` to obatin population and analyze.
