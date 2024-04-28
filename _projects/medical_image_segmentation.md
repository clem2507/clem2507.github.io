---
layout: page
title: Medical Image Segmentation
description: Medical image segmentation with UNet architectures
img: assets/img/medical_image_segmentation/cover.png
importance: 1
category: University
related_publications: false
---

This study focuses on the medical image segmentation of CT and MRI scans and serves as a course project for [IFT 3710/6759 H23 - Projets (avancés) en apprentissage automatique](https://alexhernandezgarcia.github.io/teaching/mlprojects23/). It was conducted in collaboration with my classmates, [Arthur Boschet](https://github.com/ArthurBoschet) and [Frederic Gagne](https://github.com/fregagne).

Medical image segmentation is a critical application in computer vision, providing an alternative to time-consuming and crucial tasks performed by clinicians. The U-net architecture is widely used in this field and has served as the foundation for newer architectures like Swin-UNETR, which incorporates Swin transformers blocks to achieve state-of-the-art results. Various researchers have proposed different implementations using diverse convolutional blocks or modifications to the shortcut path between the encoder and decoder.

However, comparing the effectiveness of these architectural choices can be challenging due to variations in preprocessing steps and pipeline optimizations adopted by different research teams to enhance their results. Hence, this study aims to compare proposed architectural modifications against a U-net baseline, using fixed hyper-parameters, to provide meaningful comparisons on the [Medical Image Segmentation Decathlon datasets](http://medicaldecathlon.com/) (MISD).

<div class="row justify-content-center">
    <div class="col-12">
        {% include figure.liquid loading="eager" path="assets/gif/UNet_inference.gif" title="UNet Inference Process" class="img-fluid" %}
    </div>
</div>
<div class="caption">
    UNet prediction on a validation image of the MISD heart segmentation dataset.
</div>

Through a 5-fold cross-validation analysis on the heart and lung datasets, we found that adding convolutional layers to the shortcut path showed promise as a design modification, although it did not reach statistical significance. Subsequently, we evaluated this modified model, along with the U-net baseline and Swin-UNETR, on all datasets, and found that it achieved the best overall performance, with an average rank of 1.59 across all tasks.

<div class="row justify-content-center">
    <div class="col-12">
        {% include figure.liquid loading="eager" path="assets/img/medical_image_segmentation/foldwise.png" title="Foldwise Results" class="img-fluid" %}
    </div>
</div>
<div class="caption">
    Foreground dice fold-wise difference with the U-net baseline. To evaluate the performance of various models, we calculated the foreground Dice score difference compared to the U-net baseline using a fold-wise approach. Specifically, we subtracted the training and validation foreground Dice scores of each fold of the U-net baseline model from the corresponding folds of the models under investigation, including Swin-UNETR, Half-Unet, U-net with Resblock 2, Trans-Unet, Unet-Conv-Skip, and Unet-Conv-Skip-Res2. We utilized a bootstrapping methodology to estimate the mean distribution used to compute the two-tailed p-values.
</div>

<div class="row justify-content-center">
    <div class="col-12">
        {% include figure.liquid loading="eager" path="assets/img/medical_image_segmentation/results_table_medical_seg.png" title="Segmentation Results" class="img-fluid" %}
    </div>
</div>
<div class="caption">
    This table presents the outcomes of the 5-fold cross-validation study on different models trained on both heart and lung datasets. The presented results are based on foreground dice scores, which refer to the heart class for the heart dataset and the tumor class for the lung dataset. FWD corresponds to the fold-wise difference with the U-net baseline, and the p-values indicate the probability of observing the 5-fold dice score under the U-net score distribution.
</div>

<div class="row justify-content-center">
    <div class="col-md-8">
        {% include figure.liquid loading="eager" path="assets/img/medical_image_segmentation/table_all_datasets.png" title="All Results" class="img-fluid" %}
    </div>
</div>
<div class="caption">
    The performance of three models, U-net, Swin-UNETR, and Conv-skip, on all test sets in the Medical Segmentation Decathlon is presented. The metric used to evaluate the models is the dice score, and the results are tabulated. The average rank of each model is reported to enable a comprehensive comparison of their performance.
</div>

Transformers-based models did not perform as well as convolution-based ones. It is assumed that preprocessing and aggressive data augmentation may have a crucial role in the performance reported in existing literature, and further studies incorporating these factors could help bridge the gap between our study and the existing body of work.

For more details, check out the project [report](https://clem2507.github.io/assets/pdf/MedicalSegmentationReport.pdf) and the code in our [repository](https://github.com/ArthurBoschet/medical_segmentation).