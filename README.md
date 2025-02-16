# Riffusion tuning with your songs

Riffusion tuning

So, by request, I will write a small instruction on how to train riffusion weights to your melodies. As an example, consider my experience of creating a network capable of composing songs in the style of Rammstein.

My first attempts at doing colab training failed because none of the colabs available to support special riffusion weights. But if you find such a colab, then everything will be the same

Therefore, my instruction will describe the work on the local computer

First. Actually the SD itself and the plug-in for music

First of all, you must install stable diffusion according to the instructions

https://github.com/AUTOMATIC1111/stable-diffusion-webui

Next, you need a plugin to work with music in SD

https://github.com/enlyth/sd-webui-riffusion

Also you need to download special original riffusion weights. Please note that they weigh quite a lot, but practice shows that you can shrink them, and during training they are even able to shrink up to 2 gigabytes

https://huggingface.co/riffusion/riffusion-model-v1

This way you can create music through prompts and play that music

Second. SD training

Now we need to install everything to train the neural network with our melodies

The first is a plug-in for learning neural networks on a computer, it has serious video memory limitations, you need to carefully read the description, as well as the section that indicates what settings you may need if you do not have enough video memory

https://github.com/d8ahazard/sd_dreambooth_extension

Now we need to turn our melodies into spectrograms. This will require a separate script and all the dependencies, of which there are actually a lot

https://github.com/chavinlo/riffusion-manipulation

Specifically, we need only one script from the link above, this is

https://github.com/chavinlo/riffusion-manipulation#convert-audio-to-image

Working with it is extremely simple, specify the melody, specify the folder where to put the spectrograms and run

Thus, the melody is cut into pieces of 5.1 seconds each and turns into pictures on which we can train our neural network. However, the script makes pictures in grayscale, and training is recommended to be done on RGB color pictures.

Therefore, we use any graphic application convenient for us (perhaps there are other ways, I did not specify) to convert our pictures of spectrograms from gray tones to RGB.

Note. Perhaps the conversion is not required, I can’t say here, but in order not to waste time when learning, I still recommend doing it

How many melodies do you need to learn? I took 5 Rammstein songs and each of them was cut into 40-45 segments. I threw out the first segments and the last of each melody, as well as those pieces where there were clearly sharp transitions between musical fragments of melodies (I did this by eye, analyzing the appearance of spectrograms - try it, it's very easy). This gave me exactly 200 spectrograms. Since the spectrograms on large sections of the melody do not differ much from each other, you can, if desired, remove similar ones, greatly reducing the number of duplicates and, due to this, take more songs from the desired artist

We load the resulting images with spectrograms into the dreambooth and train the original riffusion model on them.

I won’t touch on working with the dreambooth plugin, since many good instructions have already been written before me, they are both on youtube and on the page of the plugin itself.

If you do everything right, then you will have a neural network that can generate melodies in the style you want.

You can always see my version at the link, there are also examples of generated spectrograms and prompts in them

https://civitai.com/models/2669/rammstein-riffusion
