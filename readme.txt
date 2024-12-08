We implemented the paper  “Enjoy Your Editing: Controllable GANs for Image Editing via Latent Space Navigation” by Peiye Zhuang, Oluwasanmi Koyejo, Alexander G Schwing.

An example of face image editing using StyleGANv2:

-Download the StyleGAN2 weights pretrained on FFHQ dataset and put the file to /path/to/gan.
-Download the ResNet-50 classifier weights pretrained on CelebA dataset and put the file to /path/to/classifier.
-Download MobileNet weights pretrained on CelebA dataset and put the file to /path/to/MobileNet_classifier
-Modify L16 and L18 in Latent2im/graphs/stylegan_v2_real/constants.py using the above paths.
-Training command example

python /content/drive/MyDrive/EE782/Project/Latent2im-main/train.py --model stylegan_v2_real --transform face \
     --overwrite_config \
     --num_samples 2000 --learning_rate 1e-4 --latent w \
     --walk_type linear --loss l2 --gpu 0 --attrList Smiling \
     --attrPath '/content/drive/MyDrive/EE782/Project/Latent2im-main/dataset/attributes_celeba.txt' \
     --models_dir ./models_celeba # (add --overwrite_config to renew the saving folder)

-We can change num samples in the above command and batch size in constants.py in stylegan_v2_real folder.
-Attributes can be changed according to the attribute list in dataset folder, basically choose one of the attributes from that list and change attrList(-attribute) 

--Major Changes--
-Changed the pre-trained ResNet-50 model to MobileNet for regressor
-Added exponential learning rate scheduler with gamma = 0.25

--Note--
Every Result folder following naming convention as <attribute> _ <n_samps>_<batch_size> in our drive contains the following for each model: 
- output images after each epoch for selcted batches
- log.txt containing the overall performance in every iteration
- ipynb of the code
- final 10th epoch model

--Link to Project Folder--
https://drive.google.com/drive/folders/1GYYlZWK2yyaYKxT-zJAV7dnDfe7A4Cqc?usp=sharing

--Reference--
@inproceedings{ZhuangICLR2021,
  author = {P. Zhuang and O. Koyejo and A.~G. Schwing},
  title = {{Enjoy Your Editing: Controllable GANs for Image Editing via Latent Space Navigation}},
  booktitle = {Proc. ICLR},
  year = {2021},
}

