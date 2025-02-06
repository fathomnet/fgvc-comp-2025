# FGVC Kaggle Competition 2025

Navigating the Depths: Advancing Hierarchical Classification of Ocean Life

# Overview

Consider marine wildlife monitoring in coastal waters near California. Daily video footage analyzed by a standard ML model shows 2 octopuses, 1 shark, and 10 jellyfish \- broad taxonomic categories. But species-level identification could reveal crucial details. Is that an *Octopus rubescens*, commonly found in this area, or is it an *Octopus cyanea* usually only observed in warm, tropical waters near Hawai’i? Accurate species classification is essential for understanding ocean ecosystems. 

Hierarchical classification—architectures that structure data to capture relationships across taxonomic ranks (e.g., from broad categories like families to specific species)—can significantly improve classification accuracy, as demonstrated by [recent advances](https://imageomics.github.io/bioclip/) in machine learning. In the field of marine ecology, accurate taxonomic classification is essential for addressing fundamental questions: What species exist in a particular place? What is the ecosystem biodiversity and how does it change over time? Questions like these motivate the focus of our 2025 FathomNet Competition, aiming to push the boundaries of taxonomic accuracy and inspire innovative solutions in this space.

For this competition, we have curated data from the broader [FathomNet](https://fathomnet.org/fathomnet/#/) image set to tackle hierarchical classification. The training set contains 79 categories of marine animals of varying taxonomic ranks (e.g., family, genus, species), wherein 300 example instances of each category are provided for training. The test set contains the same 79 categories, where roughly 10 example instances of each category are provided for evaluation. The challenge is to develop a model that can accurately classify these taxa and ideally leverage their taxonomic information to do so. Developing these solutions for ocean research will enable scientists to process and explore ocean data more efficiently

Participants should not use other image sets to train their models outside of the Kaggle competition data and the FathomNet Database [website](https://fathomnet.org/fathomnet/#/), however they can leverage other types of outside data sources for other aspects of the competition. Pre-trained models can be used for initialization of training (e.g. [BioCLIP](https://imageomics.github.io/bioclip/), [ImageNet](https://www.image-net.org/), or [COCO](https://cocodataset.org/#home) classification or detection models provided by many deep learning packages). Teams should plan on specifying additional data sources and/or pre-trained models used when uploading results.

# Evaluation

The final test score is the mean of the hierarchical distances calculated across the test set, where the best average score is 0 and the worst is 12\. Read below to see how the hierarchical distance is calculated. 

# Submission Format

Submission format should resemble the following:

| annotation\_id | concept\_name |
| ----: | :---- |
| 1 | Ophiuroidea |

Where an annotation\_id is provided alongside a classification, or concept\_name, for each ROI. 

Submissions can be any of the following taxonomic ranks: kingdom, phylum, class, order, family,  genus, and species. These ranks are part of a **taxonomic tree**, which organizes living things into a branching structure, starting with broad groups and narrowing down to specific species. A visual representation of this can be seen below for a specific animal *Abyssocucumis abyssorum*,  

![alt text](https://github.com/fathomnet/fgvc-comp-2025/blob/main/assets/taxonomic_tree_example.png)

Submissions will be evaluated on taxonomic distance from the ground truth answer. To do so we use the [FathomNet WoRMS Module](https://fathomnet-py.readthedocs.io/en/latest/api.html#module-fathomnet.api.worms) to populate the full taxonomic name and a reference library of these taxonomic names is stored in the evaluation script. For example, if the submission concept name is *Abyssocucumis abyssorum*, the score function will populate a tree like what can be seen in the visual above.  
   
This submission is compared with the ground truth taxonomic name, and a score is given corresponding to the distance between the submission and the ground truth answer along the taxonomic tree. Example scores and visual representations are provided below.

In the following example a score of one is given, and is represented visually via the bolded line. In this case, the submission is Asteronyx of genus rank while the ground truth is *Asteronyx loveni,* which is at the species rank. The distance between the rank of the ground truth and the submission is 1, so the resulting score is 1\.  

![](https://github.com/fathomnet/fgvc-comp-2025/blob/main/assets/same_line_example.png)   

In the following example a score of six is given, and visually this can be seen in the bolded line. In this case the submission taxon is *Ophiacanthidae* of family rank while the ground truth is *Asteronyx loveni,* which is of the species rank. The distance between the rank of the ground truth and the submission is 6, so the resulting score is 6\.   

![](https://github.com/fathomnet/fgvc-comp-2025/blob/main/assets/different_rank_example.png) 

## Notes:

* If a submission name is not discoverable within the library of taxonomic names referenced in the evaluation metric, then a maximum score of 12 is assigned. This includes null submissions and misspellings.   
* Some classifications have more complex taxonomic ranks such as suborders and infraclasses. For this task, we will only consider the 7 taxonomic rankings: kingdom, phylum, class, order, family, genus, and species.  
* The ground truth categories vary in taxonomic rank.

### Competition information

This competition is presented as part of the 12th Fine-Grained Visual Categorization [(FGVC12)](https://sites.google.com/view/fgvc11) workshop at [CVPR 202](https://cvpr.thecvf.com/Conferences/2024)5 in Nashville, Tennessee.

Please feel free to open an issue on the [competition git repo](https://github.com/fathomnet/fgvc-comp-2025) if you have a question, comment, or problem. We will also respond to threads opened on the competition discussion board here on Kaggle.

### Acknowledgments

The images for this competition have been generously provided by [MBARI](https://www.mbari.org/). Annotations were made possible through the support of [FathomNet](https://www.oceanvisionai.org/) and experts from the [MBARI Video Lab](https://doi.org/10.1109/OCEANS.2006.306879). Special acknowledgment is given to Marine Biologist Linda Kuhnz for her invaluable expertise in generating a substantial portion of the groundtruth dataset.

## CVPR 2025
This competition is part of the Fine-Grained Visual Categorization [FGVC12](https://sites.google.com/view/fgvc12) workshop at the [Computer Vision and Pattern Recognition (CVPR) Conference](https://cvpr.thecvf.com/Conferences/2024). A panel will review the top submissions for the competition based on the description of the methods provided. From this, a subset of participants may be invited to present their results at the workshop. We highly encourage teams to share a public repository with their submission to aid the community in learning from one another’s approach. Attending the workshop is not required to participate in the competition, however only teams that are attending the workshop will be considered to present their work.

There is no cash prize for this competition. PLEASE NOTE: CVPR frequently sells out early, and we cannot guarantee CVPR registration after the competition's end. If you are interested in attending CVPR, please plan ahead.

You can see a list of all FGVC12 competitions [here]((https://sites.google.com/view/fgvc12).

# Data

## Dataset Description

### Data Format

The datasets are formatted to adhere to the [COCO Object Detection](https://cocodataset.org/#format-data) standard. Every training image contains at least one annotation corresponding to a `category` from 1 to 79\.

We are not able to provide images as a single downloadable archive due to [FathomNet's Terms of Use](https://fathomnet.org/fathomnet/#/license). Images should be downloaded using the indicated `coco_url` field in each of the annotation files. Participants can either use the provided `download.py` python script or write their own. The download script will save two folders: an image and a region of interest (ROI) folder. The ROI folder contains cropped images that are saved with the following file format \<image\_id\>\_\<annoation\_id\>.png while the image folder contains files saved as \<image\_id\>.png, where the ids are specified in the `dataset.json` file provided to `download.py`. 

### Files

* **`dataset_train.json`** \- the training images, annotations, and categories in COCO formatted json  
* **`dataset_test.json`** \- the evaluation images in COCO formatted json  
* **`sample_submission.csv`** \- a sample submission file in the correct format  
* **`download.py`** \- python script to download imagery from FathomNet

### Terms of Use

By downloading and using this dataset, you are agreeing to FathomNet's [Data Use Policy](https://fathomnet.org/fathomnet/#/license/). In particular:

* The annotations are licensed under a [Creative Commons Attribution-No Derivatives 4.0 International License](https://creativecommons.org/licenses/by-nd/4.0/legalcode.en).  
* The images are licensed under a [Creative Commons Attribution-Non Commercial-No Derivatives 4.0 International License.](https://creativecommons.org/licenses/by-nc-nd/4.0/legalcode.en)   
* Notwithstanding the foregoing, all of the images may be used for training and development of machine learning algorithms for commercial, academic, and government purposes.  
* Images and annotations are provided by the copyright holders and contributors "as is," and any express or implied warranties, including, but not limited to, the implied warranties of merchantability and fitness for a particular purpose are disclaimed.  
* Please acknowledge FathomNet and MBARI when using images for publication or communication purposes regarding this competition. For all other uses of the images, users should contact the original copyright holder.

For more details please see the [FathomNet Data Use Policy](https://fathomnet.org/fathomnet/#/about#datause) and [Terms of Use](https://fathomnet.org/fathomnet/#/license).

### Download

Images are made available for download by the unique URLs in the COCO-formatted object detection annotation files. The download script can be run from the command line. To install the requirements, run the following with Python >= 3.8:

```bash
pip install -r requirements.txt
```

To download the images, run the following scripts from the command line:

```bash
python download.py path/to/dataset_train.json path/to/output_dir [-n NUM_DOWNLOADS]
```
```bash
python download.py path/to/dataset_test.json path/to/output_dir [-n NUM_DOWNLOADS]
```

The optional `-n`/`--num-downloads` parameter can be used to specify the maximum number of concurrent downloads. Setting this to a value >1 can speed up the total time it takes to download the images.

> [!TIP]
> If you've cloned this repository, the COCO dataset files are available as: `dataset/dataset_train.json` and `dataset/dataset_test.json`:
> ```bash
> python download.py datasets/dataset_train.json dataset/
> ```
> ```bash
> python download.py datasets/dataset_test.json dataset/
> ```
