# IVSumm: Image and Video Summarization Library

## License
IVSUMM is Licensed under the GNU GENERAL PUBLIC LICENSE. See LICENSE for more details.

## Features and Functionalities
1) Video Summarization
- `SimpleVideoSummarizer` (using Color Histogram features)
- `DeepSimVideoSummarizer` using Features from a Deep Model and Similarity based functions
- `DeepCoverVideoSummarizer` using Features from a Deep Model and Coverage Based Functions
- `EntitySimVideoSummarizer` using Entity Models and Features from a Deep Model and Similarity based functions

2) Image Collection Summarization
- `SimpleImageSummarizer` (using Color Histogram features)
- `DeepSimImageSummarizer` using Features from a Deep Model and Similarity based functions
- `DeepCoverImageSummarizer` using Features from a Deep Model and Coverage Based Functions

## Summarization Models (-summaryModel)
- `Facility Location Functions` (Representation Models)
- `Disparity Min` and `Disparity Sum` (Diversity Models)
- `Set Cover` and `Probabilistic Set Cover` (Coverage Models)
- `Feature Based Functions`
- `Graph Cut` and `Saturated Coverage Functions`

## Summarization Algorithms (-summaryAlgo)
- `Budgeted Greedy Algorithm` (Lazy or naive greedy algorithm under a budget, say, 60 seconds)
- `Stream Greedy Algorithm` (Provide a threshold for summarization, say, 0.001)
- `Coverage Greedy Algorithm` (Provide a coverage fraction, say, 0.9 fraction of the video)

## Segment Type (-segmentType)
In the case of video summarization, we support two kinds of segmentation algorithms
- Fixed Lengh Snippets
- Shot Detection based Snippets

## Dependencies
- If you just want to compile and build `SimpleVideoSummarizer` and `SimpleImageSummarizer` examples, you only need OpenCV 3 (https://github.com/opencv/opencv)
- For running Deep Video Summarizer examples (with Caffe models), you will need to install Caffe (https://github.com/BVLC/caffe). You just need the CPU version of Caffe
- For running the Entity based Summarizers you might also need Dlib if you are using the feature extractor algorithms from dlib.

## Building and Compiling
- Modify the CMakeLists.txt to point to yout OpenCV and Caffe locations
- `mkdir build`
- `cd build`
- `cmake ..`
- `make`

## Example commands to run the executables:

SimpleVideoSummExample: DisparityMin with Budgeted Summarization 
`./SimpleVideoSummExample -videoFile <videoFileName> -videoSaveFile <videoSummaryFileName> -summaryModel 0 -segmentType 0 -summaryAlgo 0 -budget 30`

SimpleVideoSummExample: Facility Location with Budgeted Summarization
`./SimpleVideoSummExample -videoFile <videoFileName> -videoSaveFile <videoSummaryFileName> -summaryModel 2 -segmentType 0 -summaryAlgo 0 -budget 30`

SimpleImageSummExample: DisparityMin with Budgeted Summarization
`./SimpleImageSummExample -directory ~/Desktop/ivsumm/images/ -imageSaveFile ~/Desktop/ivsumm/images/summary-montage.png -summaryModel 0 -summaryAlgo 0 -budget 10 -summarygrid 100`

DeepVideoSummExample DisparityMin with Budgeted Summarization (Using GoogleNet Scene Model)
`./DeepVideoSummExample -videoFile <videoFileName> -videoSaveFile <videoSummaryFileName> -summaryModelSim 0 -simcover 0 -segmentType 0 -summaryAlgo 0 -featureLayer loss3/classifier -network_file ../../Models/googlenet_places205/deploy_places205.protxt -trained_file ../../Models/googlenet_places205/googlelet_places205_train_iter_2400000.caffemodel -mean_file ../../Models/hybridCNN/hybridCNN_mean.binaryproto -label_file ../../Models/googlenet_places205/categoryIndex_places205.csv -budget 30`

DeepVideoSummExample: Facility Location with Budgeted Summarization (Using GoogleNet Scene Model)
`./DeepVideoSummExample -videoFile <videoFileName> -videoSaveFile <videoSummaryFileName> -summaryModelSim 2 -simcover 0 -segmentType 0 -summaryAlgo 0 -featureLayer loss3/classifier -network_file ../../Models/googlenet_places205/deploy_places205.protxt -trained_file ../../Models/googlenet_places205/googlelet_places205_train_iter_2400000.caffemodel -mean_file ../../Models/hybridCNN/hybridCNN_mean.binaryproto -label_file ../../Models/googlenet_places205/categoryIndex_places205.csv -budget 30`

DeepVideoSummExample: SetCover with Budgeted Summarization (Using GoogleNet Scene Model)
`./DeepVideoSummExample -videoFile <videoFileName> -videoSaveFile <videoSummaryFileName> -summaryModelSim 0 -simcover 1 -segmentType 0 -summaryAlgo 0 -featureLayer loss3/classifier -network_file ../../Models/googlenet_places205/deploy_places205.protxt -trained_file ../../Models/googlenet_places205/googlelet_places205_train_iter_2400000.caffemodel -mean_file ../../Models/hybridCNN/hybridCNN_mean.binaryproto -label_file ../../Models/googlenet_places205/categoryIndex_places205.csv -budget 30`

DeepImageSummExample: DisparityMin with Budgeted Summarization (Using GoogleNet Scene Model)
`./DeepImageSummExample -directory ~/Desktop/ivsumm/images/ -imageSaveFile ../images/summary-montage.png -summaryModelSim 2 -simcover 0 -summaryAlgo 0 -summarygrid 100 -featureLayer loss3/classifier -network_file ../../Models/googlenet_places205/deploy_places205.protxt -trained_file ../../Models/googlenet_places205/googlelet_places205_train_iter_2400000.caffemodel -mean_file ../../Models/hybridCNN/hybridCNN_mean.binaryproto -label_file ../../Models/googlenet_places205/categoryIndex_places205.csv -budget 10`

EntityFaceSummExample: DisparityMin with Budgeted Summarization (Using Resnet Face detection and Dlib feature extractors)
`./EntityFaceSummExample -videoFile ~/Desktop/ivsumm/videos/friends.mp4 -imageSaveFile ~/Desktop/ivsumm/videos/friends-collage.png -summaryModel 0 -summaryAlgo 0 -summarygrid 60 -landmarking_model_file ~/Desktop/DNNModels/dlib/shape_predictor_5_face_landmarks.dat -pretrained_resnet_file ~/Desktop/DNNModels/dlib/dlib_face_recognition_resnet_model_v1.dat -featMode 1 -network_file_face ~/Desktop/DNNModels/ResnetFace/deploy.prototxt -trained_file_face ~/Desktop/DNNModels/ResnetFace/res10_300x300_ssd_iter_140000.caffemodel -label_file_face ~/Desktop/DNNModels/ResnetFace/labels.txt -budget 25`
