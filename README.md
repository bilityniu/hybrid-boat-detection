<img height="171px" width="340px" align="right" src="https://i.imgur.com/r7IpzX8.jpg">  

### Robust Detection of Marine Vessels From Visual Time Series

This repo contains the implementation of our work: **Robust Detection of Marine Vessels From Visual Time Series**, by Tunai Porto Marques *et al.*, accepted for presentation at the 2021 Winter Conference on Applications of Computer Vision (WACV, January 5-9, 2021). The camera-ready version of the manuscript will be released soon. 

If the software provided proves to be useful to your work, please cite its related publication: 

#### BibTeX

>    @inProceedings{TPMarques_WACV_2021,    
>      title={Robust Detection of Marine Vessels from Visual Time Series},    
>      author={Porto Marques, Tunai and Branzan Albu, Alexandra and O'Hara, Patrick and Serra, Norma and Morrow, Ben and McWhinnie, Lauren and Canessa, Rosaline},    
>      booktitle={Proceedings of the IEEE Winter Conference on Applications of Computer Vision},      
>      year={2021}}

### Installation and requirements

1. **Detectron2**. The detector was built using Facebook's Dectron2. More specifically, [conansherry's Windows build of Detectron2](https://github.com/conansherry/detectron2). Follow that repo's intructions on how to install Detectron2, [PyTorch](https://pytorch.org/get-started/locally/), torchvision, [OpenCV](https://anaconda.org/conda-forge/opencv), [fvcore](https://github.com/facebookresearch/fvcore), [pycocotools](https://github.com/philferriere/cocoapi.git#subdirectory=PythonAPI) and cython. I have also put together a [tutorial on how to install Detectron2 on Windows](https://github.com/tunai/hybrid-boat-detection/blob/master/install_detectron2_win10.md) with specific package versions which you can follow (both guides will work).  
Although not yet tested, the boat detector should work with the original Linux release of Detectron2. Once you are done, check the installation on your Python environment: 
        
```python
import detectron2
detectron2.__version__
```
You should be able to see the version of your Detectron2 (e.g., "0.1") if the installation was sucessful. 

2. Clone and install this repo and its supporting packages (with your Detectron2 python environment activated on anaconda prompt):
```
git clone https://github.com/tunai/hybrid-boat-detection
cd hybrid-boat-detection
conda install -c anaconda xlsxwriter
```
3. Test the hybrid boat detector:
```python
python main.py
```       
Your output should look like [this](https://i.imgur.com/IadQOxX.jpg) 

### Usage

#### Generic data and output structure

To run the detector with sample data, simply call ```python main.py```. The detector reads all *.jpg* and *.png* images on the subfolders inside of *"./data/"*. Each run will generate the following output on each subfolder: 

<img height="102px" width="1023px" align="center" src="https://i.imgur.com/CThe9IW.jpg.jpg">  

The highlighted images showing the final output of detected boats are located in *"./positiveHybrid/"*. The output folders also contain two *.xlsx* spreadsheets ([example](https://i.imgur.com/MXT3PQc.jpg)) that specify, for each image, how many boats were found, the detection certainty scores and individual bounding boxes coordinates (note: **OD** indicates detection using pre-trained DL-based object detectors only, while **Hybrid** indicates the final, hybrid results). 

#### Using your own data

**Preliminary considerations**: this detector was developed to use small time series of three monitoring images captured 5 seconds apart from each other using a static camera. You can try different capture layouts, but please keep in mind the system's original intent and considerations when using it. 

Place your images in subfolders inside of *"./data/"*. Each scene should be represented by a group of three images named using the following convention "prefix+YYYY-MM-DD_HH-MM-SS.format", where *prefix* is the name of the site, and *format* is either *".jpg"* or *".png"*. For example: consider a sulbfolder containing nine images (three groups of three images) for a test site called "site1": 
```
site1_2018-08-21_20-37-12.jpg
site1_2018-08-21_20-37-17.jpg
site1_2018-08-21_20-37-22.jpg
site1_2018-08-21_22-05-01.jpg
site1_2018-08-21_22-05-06.jpg
site1_2018-08-21_22-05-11.jpg
site1_2018-08-21_23-25-13.jpg
site1_2018-08-21_23-25-18.jpg
site1_2018-08-21_23-25-23.jpg
```
**Note**: you images need to be inside of **subfolders** of *"./data/"*. 

Once your images are placed in *"./data/"*, run ```python main.py``` and subfolders will be created with the outputs described above. If performing research, change the parameters of *config.py* to test different backbones, hyper-parameters, etc.  

### Repo author

Tunai Porto Marques (tunaip@uvic.ca), [website](https://www.tunaimarques.com) 



