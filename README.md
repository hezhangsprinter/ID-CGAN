## Image De-raining Using a Conditional Generative Adversarial Network
[[Paper Link](https://arxiv.org/abs/1701.05957)]   

[[Project Page](http://www.rci.rutgers.edu/~vmp93/index_ImageDeRaining.html)]



He Zhang, Vishwanath Sindagi, Vishal M. Patel


In this paper, we investigate a new point of view in addressing single image de-raining problem. Instead of focusing only on deciding what is a good prior or a good framework to achieve good quantitative and qualitative performance, we also ensure that the de-rained image does not degrade the performance of a given computer vision algorithm such as detection and classification. In other words, the de-rained result should be indistinguishable from its corresponding clear image to a given discriminator. This criterion can be directly incorporated into the optimization framework by using the recently introduced conditional generative adversarial networks (GANs). To minimize artifacts introduced by GANs and ensure better visual quality, a new refined loss function is introduced.

	@article{zhang2017image,		
	  title={Image De-raining Using a Conditional Generative Adversarial Network},
	  author={Zhang, He and Sindagi, Vishwanath and Patel, Vishal M},
	  journal={arXiv preprint arXiv:1701.05957},
	  year={2017}
	} 

<img src="image/example1.png" width="400px" height="200px"/><img src="image/example2.png" width="400px" height="200px"/>



## Prepare
Instal torch7

Install nngraph

Install hdf5
 
Download the dataset from (https://drive.google.com/drive/folders/0Bw2e6Q0nQQvGbi1xV1Yxd09rY2s?resourcekey=0-dUoT9AJl1q6fXow9t5TcRQ&usp=sharing) 
and put the dataset folder into the "IDCGAN" folder

It seems that the dataset has been maliciously deleted by someone. I will try to bring it back. In the meantime, you could also get access to another training set
https://github.com/hezhangsprinter/DID-MDN

## Training

	DATA_ROOT=./datasets/rain name=rain which_direction=BtoA th train.lua

## Testing

	DATA_ROOT=./datasets/rain name=rain which_direction=BtoA phase=test_nature th test.lua


##  Testing using ID-CGAN model
The trained ID-CGAN model  and our training and testing datasets can be found at 
(https://drive.google.com/drive/folders/0Bw2e6Q0nQQvGbi1xV1Yxd09rY2s?resourcekey=0-dUoT9AJl1q6fXow9t5TcRQ&usp=sharing)

*Make sure you download the vgg model that used for perceotual loss and put it in the ./IDCGAN/per_loss/models



##Acknowledgments##

Code borrows heavily from [[pix2pix](https://github.com/phillipi/pix2pix)]
 and [[Perceptual Loss](https://github.com/jcjohnson/fast-neural-style)]. Thanks for the sharing.
