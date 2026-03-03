Now that you know how the Brain thinks, we need to talk about how to teach it. A CNN is completely useless without Data.

In Week 2, you learned that a single image is a Matrix (NumPy array).
To train a Deep Learning model, we need thousands of these matrices, properly organized and labeled. This is called a Dataset.

Since we want to classify specific patches of skin as either "Acne" or "Clear", we are building a Binary Classifier (2 classes: 0 or 1).

The Standard ML Folder Architecture
When you use a professional Deep Learning library like TensorFlow/Keras or PyTorch, you cannot just throw 1,000 images into a random folder. The library expects a very strict directory structure. The folder names become the labels.

You will need to set up your project folder like this:

Plaintext
dataset/
│
├── train/                   <-- Used to TEACH the brain (80% of data)
│   ├── acne/                <-- Contains 800 zoomed-in images of pimples
│   └── clear_skin/          <-- Contains 800 zoomed-in images of clear skin
│
└── validation/              <-- Used to TEST the brain (20% of data)
    ├── acne/                <-- Contains 200 images the brain has NEVER seen
    └── clear_skin/          <-- Contains 200 images the brain has NEVER seen
The "Train/Validation Split" (Crucial Interview Concept)
Notice how we split the data into train and validation.

Why do we do this? Imagine I give you 10 math problems to study for an exam. You memorize the exact answers to those 10 problems. If I give you the exact same 10 problems on the final exam, you will score 100%. But did you actually learn math, or did you just memorize the paper?

If the CNN memorizes the training data, it is called Overfitting.


If we need to collect 2,000 images to put into dataset/train/acne/ to teach our CNN...
Should these images be full-face photos (like the ones from your webcam right now), or should they be tightly cropped, zoomed-in square images of just the pimple?

Tell me your engineering decision and why. Think about what those 3x3 Convolutional Filters are trying to learn!
#Answer:-
"I chose tightly cropped images to eliminate background noise and isolate the Region of Interest (ROI). If I feed the CNN a full-face image, it might falsely correlate features like my glasses, hair, or the background wall with the 'acne' class. By cropping down to a specific patch (e.g., 64x64 pixels), I force the convolutional filters to focus strictly on the structural anomalies and texture of the skin. Furthermore, I ensured all images were resized to a consistent matrix dimension to maintain tensor uniformity, and I balanced the dataset to prevent the model from developing a bias toward the majority class."

To prove the CNN actually learned what acne looks like, we must test it on the validation folder—images it has never looked at before. If it scores high on the training data but low on the validation data, your model is practically useless in the real world.
