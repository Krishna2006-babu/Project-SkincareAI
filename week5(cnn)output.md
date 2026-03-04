C:\Users\krish\AppData\Local\Programs\Python\Python311\python.exe: can't open file 'C:\\Users\\krish\\OneDrive\\Desktop\\Skincare_AI\\train_model.py': [Errno 2] No such file or directory
(venv) PS C:\Users\krish\OneDrive\Desktop\Skincare_AI> python scripts/train_model.py   
2026-03-03 17:36:11.311462: I tensorflow/core/util/port.cc:153] oneDNN custom operations are on. You may see slightly different numerical results due to floating-point round-off errors from different computation orders. To turn them off, set the environment variable `TF_ENABLE_ONEDNN_OPTS=0`.
TensorFlow Version: 2.20.0
Found 60 files belonging to 2 classes.
2026-03-03 17:36:19.364045: I tensorflow/core/platform/cpu_feature_guard.cc:210] This TensorFlow binary is optimized to use available CPU instructions in performance-critical operations.
To enable the following instructions: SSE3 SSE4.1 SSE4.2 AVX AVX2 AVX_VNNI FMA, in other operations, rebuild TensorFlow with the appropriate compiler flags.
Model: "sequential_1"
┏━━━━━━━━━━━━━━━━━━━━━━━━━━━━━┳━━━━━━━━━━━━━━━━━━━━━┳━━━━━━━━━━━━━┓
┃ Layer (type)                ┃ Output Shape        ┃     Param # ┃    
┡━━━━━━━━━━━━━━━━━━━━━━━━━━━━━╇━━━━━━━━━━━━━━━━━━━━━╇━━━━━━━━━━━━━┩    
│ sequential (Sequential)     │ (None, 64, 64, 3)   │           0 │    
├─────────────────────────────┼─────────────────────┼─────────────┤    
│ rescaling (Rescaling)       │ (None, 64, 64, 3)   │           0 │    
├─────────────────────────────┼─────────────────────┼─────────────┤    
│ conv2d (Conv2D)             │ (None, 62, 62, 32)  │         896 │    
├─────────────────────────────┼─────────────────────┼─────────────┤    
│ max_pooling2d               │ (None, 31, 31, 32)  │           0 │    
│ (MaxPooling2D)              │                     │             │    
├─────────────────────────────┼─────────────────────┼─────────────┤    
│ conv2d_1 (Conv2D)           │ (None, 29, 29, 64)  │      18,496 │    
├─────────────────────────────┼─────────────────────┼─────────────┤    
│ max_pooling2d_1             │ (None, 14, 14, 64)  │           0 │    
│ (MaxPooling2D)              │                     │             │    
├─────────────────────────────┼─────────────────────┼─────────────┤    
│ conv2d_2 (Conv2D)           │ (None, 12, 12, 64)  │      36,928 │    
├─────────────────────────────┼─────────────────────┼─────────────┤    
│ flatten (Flatten)           │ (None, 9216)        │           0 │    
├─────────────────────────────┼─────────────────────┼─────────────┤    
│ dense (Dense)               │ (None, 64)          │     589,888 │    
├─────────────────────────────┼─────────────────────┼─────────────┤    
│ dense_1 (Dense)             │ (None, 1)           │          65 │    
└─────────────────────────────┴─────────────────────┴─────────────┘    
 Total params: 646,273 (2.47 MB)
 Trainable params: 646,273 (2.47 MB)
 Non-trainable params: 0 (0.00 B)

🚀 STARTING TRAINING LOOP...
Epoch 1/10
8/8 ━━━━━━━━━━━━━━━━━━━━ 2s 19ms/step - accuracy: 0.5667 - loss: 0.7607
Epoch 2/10
8/8 ━━━━━━━━━━━━━━━━━━━━ 0s 16ms/step - accuracy: 0.5000 - loss: 0.6943
Epoch 3/10
8/8 ━━━━━━━━━━━━━━━━━━━━ 0s 16ms/step - accuracy: 0.5000 - loss: 0.6952
Epoch 4/10
8/8 ━━━━━━━━━━━━━━━━━━━━ 0s 15ms/step - accuracy: 0.4500 - loss: 0.6936
Epoch 5/10
8/8 ━━━━━━━━━━━━━━━━━━━━ 0s 15ms/step - accuracy: 0.5000 - loss: 0.7031
Epoch 6/10
8/8 ━━━━━━━━━━━━━━━━━━━━ 0s 15ms/step - accuracy: 0.4667 - loss: 0.6935
Epoch 7/10
8/8 ━━━━━━━━━━━━━━━━━━━━ 0s 17ms/step - accuracy: 0.5833 - loss: 0.6928
Epoch 8/10
8/8 ━━━━━━━━━━━━━━━━━━━━ 0s 16ms/step - accuracy: 0.5000 - loss: 0.7023
Epoch 9/10
8/8 ━━━━━━━━━━━━━━━━━━━━ 0s 15ms/step - accuracy: 0.5667 - loss: 0.6907
Epoch 10/10
8/8 ━━━━━━━━━━━━━━━━━━━━ 0s 15ms/step - accuracy: 0.5333 - loss: 0.6939
WARNING:absl:You are saving your model as an HDF5 file via `model.save()` or `keras.saving.save_model(model)`. This file format is considered legacy. We recommend using instead the native Keras format, e.g. `model.save('my_model.keras')` or `keras.saving.save_model(model, 'my_model.keras')`.

💾 Model saved as 'skin_model.h5'

📊 The Engineering Reality CheckLook closely at your final line:Epoch 10/10 - accuracy: 0.5333 - loss: 0.6939If you are in an interview and the manager asks, "Krishna, your model got 53% accuracy. Is that good?" The answer is: No. It is actually terrible, and mathematically, it means the AI is flipping a coin.Since there are only two choices (Acne or Clear Skin), a blindfolded person guessing randomly would get 50% accuracy. Your AI got 53%.Furthermore, look at your loss: 0.6939.In binary crossentropy, the mathematical formula for a model that is completely unsure and just guessing 50/50 for everything is $-\ln(0.5)$, which equals exactly 0.693.🧠 Why did this happen? (And why it's okay)Do not be discouraged. This is exactly what is supposed to happen right now. Your code is perfect, but your Data and Training Time are too small.Too Little Data: We only gave it 60 images. Modern CNNs need thousands of images to learn complex structural features.Too Little Time: We only ran it for 10 "Epochs" (loops). The model barely had time to look at the data before it was told to stop.Data Augmentation Overload: Because we flipped, zoomed, and rotated a tiny dataset, the CNN got confused. It couldn't find a consistent pattern in such a small amount of time.🛠️ The Architecture First, Intelligence LaterIn software engineering, we build the Pipeline first.Even though your skin_model.h5 is currently a "dumb" brain, it is a working brain in the correct file format.Our next step is to wire this .h5 file into your live webcam feed (inside skin_analysis.py). We need to replace your old OpenCV color-rules with this new Deep Learning model. Once the webcam is successfully talking to the CNN, making the AI "smarter" is as easy as collecting more images and changing epochs=10 to epochs=100.

