# fitness_project for Overhand Fitness
[Overhand Fitness](http://overhandfitness.cn/en/home) 
A company that offers a gamified, immersive, full-body workout, They have fun games and activities to get you moving and burning calories. They use displays and fitness trackers to measure exercise performance.    
From their website: “Using two on-wrist devices, Overhand Fitness precisely tracks and measures a person’s body movements on the X, Y, and Z axis, such as punches (counts, speed, power), jump rope, push ups, squats, burpees, jumping jacks, and many more.  This is done using sensors and advanced algorithms able to recognize the precise inertial signature of each body movement.”      

The goal of the Project and project scope: 
Data type: time series numerical data (the sensor measured at the 100 Hz= 100 data points/s)   
Features: gyro-XYZ, lowAccel-XYZ, highAccel-XYZ  
Label: exercise categories (around 15 different exercise)  
Problem type: Human Activity Recognition 
Goal: recognize the exercise type and detect the performace (the measurement)

Prerequisites  
Building environment: 
* Python [Pandas](https://pandas.pydata.org), [Numpy](http://www.numpy.org), [Plotly](https://plot.ly/ipython-notebooks/cufflinks/), [Visdom](https://github.com/facebookresearch/visdom), [Pytorch](https://pytorch.org), [Keras](https://keras.io), scikit learn 
* Database: PostgreSQL 
```
pip install numpy scikit-learn pandas jupyter 
pip3 install torch torchvision 
pip install Keras
``` 
Pipeline (Updated): 
* Data preprocessing:
   * Apply SVD and PCA to extract key features varied on specific exercise type 
   * Data normalization to get mean, std; using minmax and FFT, FIR filtering to get more data variants during repeated time chunks, window cutting, finally chosse to use DFT (discrete fourier transform) to change frequecy and time domain within the certain ampitudes, and after some algorithm research, the DWT (discrete wavelet transform) is the good fit for the mordern signal processing problem. For the window cutting, design the window sizes by interactive graphs and run the algorithms to decide which windowed sizes range is most reasonable. 
   
* Algorithm: 
   * Build the classifier SVM as the baseline model, split data into train_validation_test, implement Random Forest (RF),K-nearest neighbors (KNN) to test the accuracy, which based on small datasets. Besides apply MLP, the simplified neural networks to run the model, the code will implemented by the deep learning lib Keras, the final model hypothesis is RNN + LSTM. 
   
Related working reference: 
- CodeBook UCI Data Analysis. (n.d.). Retrieved July 23, 2018, http://ucihar-data-analysis.readthedocs.io/en/latest/CodeBook/
- Paul, J. (n.d.). Peak signal detection in real time time series data. Retrieved July 23, 2018, https://stackoverflow.com/questions/22583391/peak-signal-detection-in-realtime-timeseries-data/22640362#22640362 
