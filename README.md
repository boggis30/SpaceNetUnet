## SpaceNetUnet

This project is aimed to demonstrate how a deep learning model can be engineered and improoved.  
It is based on [SpaceNet Vegas data](https://github.com/SpaceNetChallenge/SpaceNetChallenge.github.io/blob/master/AOI_Lists/AOI_2_Vegas.md).  
Baseline model is Unet like , it is inspired by this [blog post](https://azure.microsoft.com/en-us/blog/how-to-extract-building-footprints-from-satellite-images-using-deep-learning/).  
  
Model engineering is in `notebooks` dir

Example outputs are included in the examples directory

##### Baseline
![Alt text](/examples/baseline.jpg?raw=true "Figure 1")
##### Improoved model
![Alt text](/examples/improoved.jpg?raw=true "Figure 2")


#### Download SpaceNet Vegas data
It is implied that you have a valid AWS account and installed cli.  
If you don't have cli you can download data from [aws s3 public bucket](https://s3.console.aws.amazon.com/s3/buckets/spacenet-dataset).

    aws s3api get-object --bucket spacenet-dataset \
        --key AOIs/AOI_2_Vegas/misc/AOI_2_Vegas_Test_public.tar.gz \
        --request-payer requester AOI_2_Vegas_Test_public.tar.gz  
      
    mkdir AOI_2_Vegas  
      
    tar -C AOI_2_Vegas -xf AOI_2_Vegas_Test_public.tar.gz AOI_2_Vegas  

#### Download SpaceNet utilities and install requirements

    https://github.com/SpaceNetChallenge/utilities/tree/master
      
    pip install -r utilities/python/requirements.txt
  
#### Process geo files to images

    python utilities/python/createDataSpaceNet.py 'AOI_2_Vegas' \
               --srcImageryDirectory RGB-PanSharpen \
               --outputDirectory 'AOI_2_Vegas_processed' \
               --annotationType PASCALVOC2012 \
               --imgSizePix 650 \
               --outputFileType JPEG \
               --convertTo8Bit  
      
    mkdir tiles
      
    cp AOI_2_Vegas_processed/annotations/.*jpg AOI_2_Vegas_processed/annotations/.*segcls.tif' tiles  
    
      
At this point you should have 3851 satellite images and 3851 corresponding building footprint masks.