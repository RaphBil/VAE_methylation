# Variational Autoencoder applied to genome-scale DNA methylation data
This repository is adapted from the [Tybalt](https://github.com/greenelab/tybalt) repository developed by Way et al. This repository is a fork of the previously mentioned repo, but due to a technical error, it was uploaded to GitHub independently. 
 
## Alexander Titus 2018 -- extended from Gregory Way 2017

This script trains and outputs results for a variational autoencoder (VAE) applied to genome-scale breast cancer methylation data measured using the Illumina 450K bead array. A VAE is an unsupervised learning approach that given input data uses data generation to approximate a lower dimensional representation of the input. Whether the lower dimensional representation (or manifold) of the input can contribute to improved understanding of cancer biology will require comparison to other approaches. Nonetheless, opportunities to interrogate the latent space in the VAE generative model also motivate the application of these methods to high-dimensional data such as DNA methylation data. 

The model trained here used methylation data measured with the 450K Illumina array that was subset to the 100,000 CpGs whose methylation was most variable (median absolute deviation). The VAE approach then sampled a noise vector to reparameterize the encoded space and compress to vectors of length 100 for mean and variance. The 100 encoded layers can then be used to reconstruct the original input data. The encoding scheme uses relu activations and the decoder uses a sigmoid activation to enforce positive activations. All weights are glorot uniform initialized.

To encourage manifold learning, the model also uses warm start as discussed in Sonderby et al. 2016 and an added parameter beta, to control KL divergence loss that is contributed to total VAE loss (reconstruction + (beta * KL)). In this setting, the model begins training deterministically as a plain autoencoder (beta = 0) and slowly ramps up after each epoch linearly to beta = 1. After a parameter sweep, Way et al. observed that kappa has little influence in training, therefore, we set kappa = 1, which is a full VAE.
