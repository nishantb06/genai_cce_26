#### Reducing the dimensions of MNIST dataset
```python
# Reduce the dimension using PCA
import numpy as np
import matplotlib.pyplot as plt
from sklearn.mixture import GaussianMixture
from torchvision import datasets

mnist = datasets.MNIST(root='./data', train=True, download=True)
X = mnist.data.numpy()
y = mnist.targets.numpy()
# Convert to float
X = X.astype(np.float32) / 255.0
# Flatten 28x28 -> 784
X = X.reshape(len(X),-1)
print("Dataset Shape",X.shape)

from sklearn.decomposition import PCA

pca = PCA(n_components=20)
X_pca = pca.fit_transform(X)
print("Reduced Shape of Data ",X_pca.shape)
```

