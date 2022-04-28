# Iris Flower Classification

Iris flower classification based on the size of petal and sepal using **K-Nearest Neighbors (KNN)**

<img class="img-modal-src" src="project-iris-flower/iris-pair-plot.png?raw=true" alt="Iris - Data Distribution">

Since the KNN algorithm uses distance measurements, **feature scaling** is mandatory.

<img class="img-modal-src" src="project-iris-flower/iris-hist.png?raw=true" alt="Iris - Histogram">

I'm using **min-max scaler** (MinMaxScaler) for this project because the data distribution is not normal. And then, I use a **grid search** to find the best hyperparameter.

<img class="img-modal-src" src="project-iris-flower/iris-confusion-matrix-gs.png?raw=true" alt="Iris - Confusion Matrix" width="70%">

After using the best hyperparameter, I got **100% accuracy!**

<a href="https://www.kaggle.com/code/adhang/iris-flower-classification-knn-100-accuracy" target="_blank">Iris Flower Classification</a>