# Waterloo-Point-Cloud-Database-6.0

This database was created by Honglei Su ([suhonglei@qdu.edu.cn](mailto:suhonglei@qdu.edu.cn)) and Juncheng Long ([jeasonloong@gmail.com](mailto: jeasonloong@gmail.com)) from Qingdao University in 2024. We welcome everyone to carry on the test and propose the modification opinion. If you use our database [WPC6.0](https://drive.google.com/drive/folders/1ih50PQgqZDK7wyDGAzBp-u-Kg-PL7IZi?usp=drive_link) (a Google account required) in your paper, please cite our paper:

@article{long2024perceptual,  
  title={Perceptual Quality Assessment of Trisoup-Lifting Encoded 3D Point Clouds},  
  author={Long, Juncheng and Su, Honglei and Liu, Qi and Yuan, Hui and Gao, Wei and Song, Jiarun and Wang, Zhou},  
  journal={arXiv preprint arXiv:2410.06689},  
  year={2024}  
}

The WPC6.0 database is composed of 400 Trisoup-Lifting encoded point clouds and corresponding bitstreams whose original point clouds (Bag, Banana, Biscuits, Cake, Cauliflower, Flowerpot, House, Litchi, Mushroom, Ping-pong_bat, Puer_tea, Pumpkin, Ship, Statue, Stone, Tool_box) are from the [WPC database](https://github.com/qdushl/Waterloo-Point-Cloud-Database). Each original point cloud is encoded by 4 geometry parameters tNSL {3, 4, 5, 6} and 5 texture parameters QP {28, 34, 40, 46, 51} at G-PCC Trisoup-Lifting mode. The rest of the encoding parameters are set with default values. The subjective test settings and raw data processing are the same as those in the WPC database.

# streamPCQ-TL model

In order to extract parameters of streamPCQ-TL model from bitstream of distorted point cloud, we have reformed the source code files from mpeg-pcc-tmc13-release-v23.0-rc2 ([release-v23.0-rc2](https://github.com/MPEGGroup/mpeg-pcc-tmc13/tree/release-v23.0-rc2)). We use the reformed version to realize predicting perceptual quality of distorted point cloud without the need for fully decoding. And the modifications are applied to PCCTMC3Decoder.h, decoder.cpp and TMC3.cpp in tmc3 project. Moreover, we introduce two new files, streamPCQ.h and streamPCQ.cpp, to construct the streamPCQ-TL model and modify CMakeLists.txt to compile the two files into tmc3 project. It should be noted that the refactor version soley adds streamPCQ-TL model into tmc3 project and other code remain the same as in tmc3 project. And the method to use it is completely identical to method of application of mpeg-pcc-tmc13-release-v23.0-rc2 (cmake, generate solutions, use generated tmc3.exe to encode or decode point cloud). The difference is that the reformed version will output perceptual quality of point cloud encoded by Trisoup-Lifting in terminal window at work mode of decoding. We also provide a tmc3.exe generated by settings as above. Note that we change the file name of the generated tmc3.exe to streamPCQ_TL.exe.

If you have any specific questions about the reformed version, feel free to ask.


# Running
There are several examples of usage for perceptual quality assessment of a single point cloud or multiple point clouds. Note that the used streamPCQ_TL.exe as follows is generated by settings in section **streamPCQ-TL model**.
#### Single assessment

For perceptual quality assessment of a single point cloud stream, open a terminal window in the working directory and execute the following script:
```console
streamPCQ_TL.exe -c decoder.cfg --compressedStreamPath="your_file_name.bin" --reconstructedDataPath=" your_file_name.ply"
```

#### Batch assessment

For perceptual quality assessment of batch point cloud streams, we provide a corresponding batch file streamPCQ_TL.bat. Simply put point cloud stream files to assess, decoder.cfg, streamPCQ_TL.exe and streamPCQ_TL.bat in a same folder, double-click streamPCQ_TL.bat to perform perceptual quality assessment of all point cloud stream files in the current folder. And the assessment results are saved in streamPCQ_TL_predMOS.xlsx.

#### Demo

We provide a corresponding demo folder. Double-click the streamPCQ_TL.bat file in the demo folder to predict the perceptual quality of all point cloud stream files in the current folder. The prediction results will be saved in a file (streamPCQ_TL_predMOS.xlsx) in the current folder.<br/><br/>
***-----------COPYRIGHT NOTICE STARTS WITH THIS LINE------------***
***Copyright (c) 2024 The Qingdao University All rights reserved.***

Permission is hereby granted, without written agreement and without license or royalty fees, to use, copy, modify, and distribute this database (the point clouds, the results and the source files) and its documentation for any purpose, provided that the copyright notice in its entirity appear in all copies of this database, and the original source of this database, Intelligent Multimedia Signal Processing (IMSP) Laboratory at Qingdao University, is acknowledged in any publication that reports research using this database.<br/>
***Additional Restrictions for streamPCQ-TL Model:***

The streamPCQ-TL model is intended for non-commercial academic research use only. Any use of the streamPCQ-TL model for commercial purposes is strictly prohibited without the prior written consent of Qingdao University. Redistribution or modification of the streamPCQ-TL model for commercial gain is not allowed.<br/>
***-----------COPYRIGHT NOTICE ENDS WITH THIS LINE------------***

# Acknowledgment

This project is based on [G-PCC](https://www.mpeg.org/standards/MPEG-I/9/) of [MPEG](https://www.mpeg.org), thanks for their excellent works.

