# VDTEST
My solution for the Visidon application test. Using Pix2Pix
Using the PyTorch CycleGAN and pix2pix repo:
https://github.com/junyanz/pytorch-CycleGAN-and-pix2pix

## Why Pix2Pix?
Allows for many possibilities.

## Preparing data
Pix2pix training required paired images. 

command for training
python train.py --dataroot mydata/AB --name visidonfinal --model pix2pix --direction AtoB
command for testing
python test.py --dataroot mydata/AB/test --name visidonfinal --model test --netG unet_256 --dataset_mode single --norm batch --preprocess none
