# VDTEST
My solution for the Visidon application test. Using Pix2Pix
Using the PyTorch CycleGAN and pix2pix repo:
https://github.com/junyanz/pytorch-CycleGAN-and-pix2pix

## Why Pix2Pix?
Allows for many possibilities.

## Preparing data
Started with seperating input and target images and placed them in a folder called mydata (./mydata). Input and target images must be the same size and name. Using [PowerToys](https://learn.microsoft.com/en-us/windows/powertoys/) to remove "_target" and "_input" from the image filenames. Input to mydata/A/train and target to mydata/B/train. Pix2pix training required paired images so used the combine_A_and_B.py module in the datasets folder.

Data now looks like this:
![Data](https://user-images.githubusercontent.com/40422650/206715316-20211c0d-aad1-4af9-bacd-34b5ba2bdf3b.png)

## Training
Installed [Visdom](https://pypi.org/project/visdom/0.1.7/) to view training results and loss plots.
Used the default batch size 1 and 256x256 resolution because of VRAM limitations. Saw peaks at 6,5 GB / 8,0 GB vram.

Used train command:

```
python train.py --dataroot mydata/AB --name visidonfinal --model pix2pix --direction AtoB
```

Trained for 200 epochs.
Results while training:

A = input
B = target

![epoch1](https://user-images.githubusercontent.com/40422650/206721350-dd966d9c-4b43-48cc-a01a-484dfee72bd4.png)

![epoch10](https://user-images.githubusercontent.com/40422650/206721556-4b26d448-c24c-4e2e-95d6-085752b28aa7.png)

![epoch50](https://user-images.githubusercontent.com/40422650/206721753-b6201a2a-348d-4380-a0fb-aa19ded234e5.png)

![epoch100](https://user-images.githubusercontent.com/40422650/206721798-f517d2f4-d3b8-4e83-a8f2-aca853380cd7.png)

![epoch200](https://user-images.githubusercontent.com/40422650/206721893-5a16678d-7ee4-44de-a6e3-41e14c931722.png)


**Training took around 3-4 hours with a 6 year old GTX 1080. Speed could be much improved with higher batch count and more GPUs.**

## Testing

Placed the 1207 input images in the mydata/AB/test folder.

Used test command:
```
python test.py --dataroot mydata/AB/test --name visidonfinal --model test --netG unet_256 --dataset_mode single --norm batch --preprocess none --num_test 1207
```
Using --preprocess none to prevent final images from being cropped to 256x256 (resolution used to train the model)

Processing took a couple of minutes for 1207 images.

Result examples:
![results](https://user-images.githubusercontent.com/40422650/206726092-f2aea02e-b270-475a-8cc0-c5f6d6f6ea5d.png)

**Trying with my own images**

1920x1920 picture as input:

![juissi](https://user-images.githubusercontent.com/40422650/206731786-4a668089-dfa2-43f0-83d6-b92c07699ca4.png)

1024x1024 picture as input:

![lasi](https://user-images.githubusercontent.com/40422650/206731596-8d092758-9a65-4a62-8165-8eae0f9cf1cb.png)


Quality might be suffering on higher res images because model was trained on 256x256. Could be improved by using different preprocessing settings to train at higher res.


![image](https://user-images.githubusercontent.com/40422650/206737575-a0164836-7f0e-44ad-bc34-8d2ec48ee8a6.png)

## Accuracy


