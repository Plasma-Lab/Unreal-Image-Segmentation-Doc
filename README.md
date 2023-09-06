# Unreal Image Segmentation Plugin

Welcome to the documentation for the [Unreal Image Segmentation plugin](https://www.unrealengine.com/marketplace/en-US/product/image-segmentation-for-machine-learning), an Unreal Engine plugin that allows to generate data to train your semantic segmentation algorithms. This plugin is designed to make it easier and more efficient for data scientist to collect and label computer vision data.

## Prerequisites
First, go to your project settings, search for **"Custom Depth-Stencil Pass"** and set it as **"Enabled With Stencil"**.

When creating a project, avoid creating an Architecture project as they contains uncompatible settings.

Optionnaly, if you'd like to generate data while unreal is in the background you should go to Editor Preferences, search for **"Use Less CPU when in Background"** and uncheck it.

## Labeling Actors
For each element in your scene you wish to label, add two ***actor tags*** to your element's actor: the first tag is your label (e.g., "car"), and the second tag must be "seg". 

![Labeling Actors](https://github.com/Plasma-Lab/Unreal-Image-Segmentation-Doc/blob/main/images/tags.PNG?raw=true)

All elements in the scene that hasn't been tagged will be labeled as the “empty” category (index 0).

## Testing Segmentation
> To see the plugin content, do not forget to activate "Show plugin content" in your Content Broser settings.

To test the segmentation, drop the **"BP_Segmentation_test"** blueprint in your scene and press play in the editor. You will see the segmentation colors.
All elements that you haven't tagged will still display their original materials, do not worry, they are still segmented as the “empty” category in the final exports.

> **Do not forget** to remove this blueprint from the scene **before** taking captures.

![test picture](https://github.com/Plasma-Lab/Unreal-Image-Segmentation-Doc/blob/main/images/test.PNG?raw=true)

## Capturing Results:

To take captures, go to the plugin content folder and drop the **"BP_Image_Seg_Camera"** in your scene, which will serve as a camera. You can view what the camera sees by opening the **"RT_renderTarget_ImgSeg"** render target in the Utils folder. Set the angle and the position of your camera like you would with a normal camera.

You can set up your own movements for the camera, such as placing it on the hood of an AI car or place it behind your controler pawn and move your character around while captures are being taken.

![Place the camera](https://github.com/Plasma-Lab/Unreal-Image-Segmentation-Doc/blob/main/images/BP_camera.PNG?raw=true)

When you are ready to generate your dataset, you have to ways of capturing data:

- Automatic: open the plugin in Window > Image Segmentation. Select the folder where you want to save your captures, the time between each capture, and the number of captures. Press play in the editor, and then press capture.
- Manual: use the Take Screenshots blueprint.

  

## Results

The plugin will generate two folders and one CSV file. The CSV file contains the indexes of your labels.
The "images" folder contains the unprocessed screen captures. The "labels" folder contains PNG files containing the labels of your objects encoded in the Red channel of the image. Please note that this file won't open with a normal image viewer. An included Python notebook file will show you how to display the label image and how to use it with an image segmentation model.



# FAQ

## What king of meshes can I label? 

You can label most kinds of meshes, including static mesh, skeletal mesh, sky sphere, and spline mesh. However, please note that you cannot attribute a label to landscapes, so it is recommended to avoid using them. If you must use a landscape element in your scene, you can export it as a mesh and re-import it.


## My label images are black, what is going on?

The plugin is producing a PNG image containing the class of the object in the red channel (first channel). You will not be able to open it with an image viewer.


## Can I change the resolution of my captures?

Yes you can! The plugin default to a 1024 x 1024 capture window. To edit the capture size, go to the "utils" folder and open both **RT_renderTarget_ImgSeg** and **RT_renderTarget_ImgSeg_PP**.
You can edit the size of the capture in each window, do not forgot to do it on both!

![Edit camera size](https://github.com/Plasma-Lab/Unreal-Image-Segmentation-Doc/blob/main/images/size.PNG?raw=true)
