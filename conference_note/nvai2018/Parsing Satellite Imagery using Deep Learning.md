## Parsing Satellite Imagery using Deep Learning

### Procedures
    1. Pre-Processing
    2. Deep Learning data generation
    3. Post-Processing


### Objectives
* Generation of community maps
    * buildings and Roads
* Updating maps
* Building properties extraction
    * Building Dimensions + height -> 3D map
* city and urban planning

### Data Sources
* Staellite Data Source
* Ground Truth Source
    * opensource map

### Issues with training data
* Missing data, Misalignment, Bad Data
    > To solve Problem : 수작업

* Pipeline
    1. Pre-Processing
        1. Neural Enhance
        2. SRGAN
        3. Data Augmentation
        > Improving qualitiy of the data /w GAN
        >> 5%정도의 정확도 개선이 있었다.

    2. Deep Learning
        1. Semantic and Instance segmentation
        2. based on U-Net
    3. Post-Preocessing
        1. On Raster Data
            * False Positive prediction
            * Better & Thicker Boundaries
        2. On Vector Data
            * Simpify and transform a complex geometric shape to regular and simple shape.

`Dabeeo API`
