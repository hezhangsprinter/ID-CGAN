# ID-CGAN

[[Arxiv](https://128.84.21.199/abs/1701.05957)]

Image De-raining Using a Conditional Generative Adversarial Network

He Zhang, Vishwanath Sindagi, Vishal M. Patel


In this paper, we are investating a new point new in addressing single image de-raining problem. Instead of focusing only on deciding what is a good prior or a good framework to achieve good quantitative and qualitative performance, we also ensure that the de-rained image itself does not degrade the performance of a given computer vision algorithm such as detection and classification. In other words, the de-rained result should be indistinguishable from its corresponding clear image to a given discriminator. This criterion can be directly incorporated into the optimization framework by using the recently introduced conditional generative adversarial networks (GANs). To minimize artifacts introduced by GANs and ensure better visual quality, a new refined loss function is introduced.

![]({{site.baseurl}}//1_auto.jpg)