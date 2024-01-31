# Brain-tumor-analysis

- Telemaco Terzi
- Simone Vendramini
- Tommaso Ferrario

## Dataset

For the realization of this project a dataset was used for the identification
of brain tumors.\
The dataset used can be found on [kaggle](https://www.kaggle.com/datasets/jakeshbohaju/brain-tumor).

## Features explanation [[1](https://www.scirp.org/pdf/JSIP20120200017_13782492.pdf)] [[2](https://juliaimages.org/ImageFeatures.jl/stable/tutorials/glcm/)]

The dataset comprises **Magnetic Resonance Images** (MRI) of the brain, from which
all features are extrapolated using image processing techniques and gray-level
texture information and recorded in the CSV file.\
The features are described by basic image informations and hu-moments, to put in
easier words properties of an image region by exploiting space relations
underlying the gray-level distribution of a given image.\
Hu-moments capture basic information such as the area of the object, the centroid,
the orientation, and other desirable properties.

- **First Order Features**: this features provide information related to the gray-level
  distribution of the image. In particular, the following first-order features were extracted:

  - **Mean**: mean of total pixels.
  - **Variance**: variance of total pixel.
  - **Standard Deviation**: standard deviation of total pixels.
  - **Skewness**: is the asymmetry of probability distribution of pixels, it's
    defined by a real number, if it's positive the mean is near right tail,
    otherwise the mean is near left tail.
  - **Kurtosis**: quantify with a real number how much flatten tail are, if it
    negative tails are more flatten than a normal distribution, while if is negative,
    tails are less flatten than a normal distribution, in the end if it is 0
    tails are similar to normal distribution.

- Second Order Features: However they do not give any information about the relative
  positions of the various gray levels within the image.

  - **Contrast**: measure of local level variations of the pixel values.
    This features takes high values for image of high contrast.
  - **Energy**: Energy provides a measure of the heterogeneity or variation of
    intensities in the image. Images with smoother textures and less intensity
    variation will have lower energy, while more structured and significantly
    varying images will have higher energy.
  - **ASM** (_Angular second moment_): measures the smoothness of the image.
    The less smooth the region is, the more uniformly distributed are the gray
    lavel and the lower will be the value of ASM.
  - **Entropy**: measure of randomness of the values of the gray lavels and
    takes low values for smooth images.
  - **Homogeneity**: measure takes high values for low-contrast images.
  - **Dissimilarity**: that describes how often different combinations of pixel
    intensity values occur in an image. A higher dissimilarity value indicates
    that the image has more variations in intensity between neighboring pixels,
    suggesting a more complex or textured appearance.
  - **Correlation**: measure of correlation between pixels in two different directions.
  - **Coarseness**: indication of how the image is characterized by regions
    of homogeneous intensity or more abrupt transitions, thus helping to describe
    the degree of "coarseness" or "fineness" of the texture present in the image

- **Image**: defines image name.
- **Class**: defines either the image has tumor or not (1 = Tumor, 0 = Non-Tumor).


## Feature analysis

In our scenario we are solving a classification problem, therefore when we read
the dataset we convert every column in float64 and target column in category type.
<!-- image on type column -->

Morover, we can see if exists instances with null values in this way. 
<!-- image on counting null elements -->

In addition, we can study the composition of the dataset, so we can first see if the dataset is balanced.
<!-- image on plotting target class -->



### Feature extraction
The Datatset has a total of 12 features, as we explaned before, lots of features 
are computed in similar way of other. With this hypotesis, we can suppose to study
dipendencies among features to recognize correlation between them. Here you can
see the correlation matrix of features.

<!-- Correlation matrix of feature -->

Correlation matrix highlights strong correlations ($|corr[f_1,f_2]|\ge 0.75$) between:
- mean x variance
- variance x standard deviation
- variance x standard deviation
- entropy x homogeneity
- entropy x asm
- entropy x energy
- skewness x kurtosis
- contrast x dissimilarity
- energy x homogeneity
- energy x asm
- asm x homogeneity
- homogeneity x dissimilarity

With this osservation we can consider just a feature from a pool of correlated
feature, so we can pass from 13 features to 5:

- mean or variance or standard deviation
- entropy or homogeneity or asm or energy
- skewness or kurtosis
- contrast or dissimilarity
- correlation

