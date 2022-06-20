# Semantic Classification for Satellite Imagery
## About
This repository aims to perform pixel wise image segmentation of buildings using a dataset containing top-down satellite images of cities in Dubai.

The dataset used during training can be found [here](https://www.kaggle.com/datasets/humansintheloop/semantic-segmentation-of-aerial-imagery).
All images are composed by an original satellite photo, as well as a labeled mask image, with different colors corresponding to different elements, such as:
1.  Building: #3C1098 (dark purple)
2.  Land (unpaved area): #8429F6 (magenta)
3.  Road: #6EC1E4 (cyan)
4.  Vegetation: #FEDD3A (yellow)
5.  Water: #E2A929 (orange)
6.  Unlabeled: #9B9B9B (gray)

An example pair is as follows:
![Example image](https://storage.googleapis.com/kagglesdsdata/datasets/681625/1196732/Semantic%20segmentation%20dataset/Tile%201/images/image_part_003.jpg?X-Goog-Algorithm=GOOG4-RSA-SHA256&X-Goog-Credential=databundle-worker-v2@kaggle-161607.iam.gserviceaccount.com/20220619/auto/storage/goog4_request&X-Goog-Date=20220619T213428Z&X-Goog-Expires=345599&X-Goog-SignedHeaders=host&X-Goog-Signature=21b243e495a8b1bde413c751f72b002dd10cdb5035ec15203926451d02e98cc429b8e304231d9ce97b30558e34a37e2a2724ea164b409c31dd7ad49820eacbef53c35b085c7e23e29848f3f2bec56c9d552230be1dbff3fe18bd7c03b4c13ddd4ffdaaa73c633d1d6f7ec637a8b9119b8aa91d4eeb78ad64323f3734ea255f0b10c801a0e0ce00e252087bde8b0364314cfd587fad86896463c560ba2e2030913984faf3908ea17448ead98f74f9cc025f27f27b252b294adaa95c692caafacc877153bb988bc2bfc3bb4ff60cbe617ef203106614468310852446a134bb0896486db7d48b4c923190e43be8f93a71e1e26bccd3f3df246f5c76e17918d3e402)

![Example mask](https://storage.googleapis.com/kagglesdsdata/datasets/681625/1196732/Semantic%20segmentation%20dataset/Tile%201/masks/image_part_003.png?X-Goog-Algorithm=GOOG4-RSA-SHA256&X-Goog-Credential=databundle-worker-v2@kaggle-161607.iam.gserviceaccount.com/20220619/auto/storage/goog4_request&X-Goog-Date=20220619T213447Z&X-Goog-Expires=345599&X-Goog-SignedHeaders=host&X-Goog-Signature=3cf7b0c9e49c653871803dcae5ba3fbfc1e5e6960723a23bbba94752acec609f1636bd205a9ec3fe6a583297ff40acab3353e3467f33c3dc58135f066ba169c8b2f8b58a1b38d2501b279beb84bd7a425423a0b22b7712ecce898346c2f5d55f29a6726a0f60f34eb005e8c40873db02be21d407b4fa970085038ce4164748d393797bcafce7a3e0908fea14a67e46d856c23f4a968dd6af7326206f3ab96c14af59b952da605f13bdaad664ff6d30488bd7dcbb1c4995e910b5a99126b42a45a1ceb77ac8cfda8dc86648ee36000fcf2cc42dab2a29acaf29f5979b843003162c4e2028dc39dae1c41ba5a94bf9ee304797ee80738d8ccfcd0c6a7cd5b4c78b)
## Image Descriptors
Firstly, we applied image description methods as to evaluate the overall correctness and quality of the original image. As all images were taken by satellites, they are expected to have at least some small kind of degradation, so studying them beforehand by using histograms and texture analysis gives some direction as to which pre-processing methods to use.

Firstly, we used LBP to generate a texture feature histogram of some images in the dataset, trying to find some feature that best described the buildings view we are trying to find.
Next, we loaded some images using the HSV channel, as to observe the saturation and hue channels and decide if the images needed some kind of contrast correction.
Finally, we generated a histogram for each color channel to verify that the images really had some kind of noise.


## Image Pre-processing
After having visualized the images in the HSV channel, we applied a contrast enhancement algoritm and tweaked the saturation channel of each image to try and achieve a better result during the segmentation training part, as most images had overall low color change in the borders in the saturation channel view.

We also applied a denoising algorithm to remove noise generated by the satellite photography.


# Reproducing and testing
The dataset is stored under the `data` folder, and each `Tile` subfolder has a *images* and a *masks* folder, with JPG and PNG files respectively.

Run the preprocess.py script methods to preprocess and analyze images in the `data` folder.


// TODO:
View the segmentation classes available in the edisciplinas page, and implement a crude approach to a semantic classification task.
Evaluate if the obtained results correspond to a an acceptable precision rate, and decide if segmentation using a UNet or a CNN is necessary.
