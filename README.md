## MDPM: *Mid-level Deep Pattern Mining*

### Introduction
This repository contains the source code of the algorithm described in a [CVPR 2015](http://www.pamitc.org/cvpr15/) paper 
[Mid-level Deep Pattern Mining](http://www.cv-foundation.org/openaccess/content_cvpr_2015/papers/Li_Mid-Level_Deep_Pattern_2015_CVPR_paper.pdf) 
and also a technical report [Mining Mid-level Visual Patterns with Deep CNN Activations](http://arxiv.org/abs/1506.06343). More details are provided on the [project page](https://cs.adelaide.edu.au/~yaoli/?page_id=234).
This package has been tested using Matlab 2014a on a 64-bit Linux machine. This code is for research purposes only. 

### Citing MDPM

If you find MDPM useful in your research, please consider citing:

    @inproceedings{LiLSH15CVPR,
        author = {Yao Li and Lingqiao Liu and Chunhua Shen and Anton van den Hengel},
        title = {Mid-level Deep Pattern Mining},
        booktitle = {Computer Vision and Pattern Recognition},
        year = {2015}
    }

### Installing MDPM
0. **Prerequisites** 
 0. [Caffe](http://caffe.berkeleyvision.org/): install Caffe by following its [installation instructions](http://caffe.berkeleyvision.org/installation.html). 
    Do not forget to run `make matcaffe` to compile Caffe's Matlab interface. You also need to download the ImageNet mean file (run `get_ilsvrc_aux.sh` from `data/ilsvrc12 `).
    Note: As we only use Caffe CNN as a feature extractor, installing Caffe using the CPU mode is OK. 
 0. CNN models. We use consider two CNN models in the experiment. The first one is BVLC Reference CaffeNet (CaffeRef for short), 
    this model can be downloaded by running `download_model_binary.py models/bvlc_reference_caffenet` from `scripts`.
    The second is VGG 19-layer Very Deep model (VGGVD for short), which can be downloaded from [here](http://www.robots.ox.ac.uk/~vgg/research/very_deep/). 
 0. [Apriori algorithm](http://en.wikipedia.org/wiki/Apriori_algorithm): we use [this implementation](http://www.borgelt.net/src/apriori.tar.gz). Click the link to download this package. You need 
    to uncompress it and run `make` to compile it in the `apriori/apriori/src`. 
    Detailed usage of this package can be found [here](http://www.borgelt.net/doc/apriori/apriori.html).
 0. [Liblinear](http://www.csie.ntu.edu.tw/~cjlin/liblinear/): download liblinear and compile it by following its instructions. 
 0. [KSVDS-Box v11](http://www.cs.technion.ac.il/~ronrubin/Software/ksvdsbox11.zip): as we use the `im2colstep` function in this toolbox, 
     you need to download and compile it (`im2colstep` is found in `ksvdsbox11/private`).
0. **Configuring MDPM**
 0. Download MDPM: `git clone https://github.com/yaoliUoA/MDPM`.
 0. Download MIT Indoor dataset from [here](http://web.mit.edu/torralba/www/indoor.html).
 0. Open `init.m` in the Matlab. Change values of sereval variables based on your configuration, including `conf.pathToLiblinear`, `conf.pathToCaffe`, `conf.dataset` and `conf.imgDir` based on your
    local configuration. 
 0. Copy the executable file `aprior` under directory `apriori/apriori/src` and paste it under `mining` directory.    
 0. Copy the mex file `im2colstep` and paste it under `cnn` directory. 
0. **Runing MDPM**
 0. Run the `demo.m`. It should be working properly if you have followed aforementioned instructions. 
 0. **Important:** It may takes some time to get the final classification result, so it is suggested to run MDPM on a cluster 
   where jobs can be run in parallel. The `*.sh` scripts are provided to submit jobs on a cluster. 

### Pre-computed image features
0. **MIT Indoor dataset**
 0. [feature_MITIndoor_CaffeRef](http://cs.adelaide.edu.au/~yaoli/wp-content/projects/MDPM/data/feature_MITIndoor_CaffeRef.zip) and 
    [feature_MITIndoor_VGGVD](http://cs.adelaide.edu.au/~yaoli/wp-content/projects/MDPM/data/feature_MITIndoor_VGGVD.zip).
    After uncompressing the downloaded file,  copy the `.mat` files to `data/MIT67/feaFinal_128_32_150` directory, you should be able to run `classify.m`
    under `classify` to reproduce the classification result in the paper.  
0. **PASCAL VOC 2007 dataset**
 0. [feature_VOC2007_CaffeRef](http://cs.adelaide.edu.au/~yaoli/wp-content/projects/MDPM/data/feature_VOC2007_CaffeRef.zip) and 
    [feature_VOC2007_VGGVD](http://cs.adelaide.edu.au/~yaoli/wp-content/projects/MDPM/data/feature_VOC2007_VGGVD.zip).
    After uncompressing the downloaded file,  copy the `.mat` files to `data/VOC2007/feaFinal_128_32_150` directory, you should be able to run `train_VOC.m`
    and then `test_VOC.m` under `classify` to reproduce the classification result in the paper. 
0. **PASCAL VOC 2012 dataset**
 0. [feature_VOC2012_CaffeRef](http://cs.adelaide.edu.au/~yaoli/wp-content/projects/MDPM/data/feature_VOC2012_CaffeRef.zip) and 
    [feature_VOC2012_VGGVD](http://cs.adelaide.edu.au/~yaoli/wp-content/projects/MDPM/data/feature_VOC2012_VGGVD.zip).
    After uncompressing the downloaded file,  copy the `.mat` files to `data/VOC2012/feaFinal_128_32_150` directory, you should be able to run `train_VOC.m`
    and then `test_VOC_txt.m` under `classify`. The generated .txt files can be submitted to the [evaluation server](http://host.robots.ox.ac.uk:8080/accounts/login/?next=/eval/upload/). 

### Feedback

If you have any issues (question, feedback) or find bugs in the code, please contact yao.li01@adelaide.edu.au.

