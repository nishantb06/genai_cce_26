```python
# ============================================================

# Beta-VAE on MNIST using MLP Encoder and Decoder

# ============================================================

  

import torch

import torch.nn as nn

import torch.nn.functional as F

from torch.utils.data import DataLoader

from torchvision import datasets, transforms

import os

  
  

# ------------------------------------------------------------

# Device setup

# ------------------------------------------------------------

device = torch.device("cuda" if torch.cuda.is_available() else "cpu")

print("Using device:", device)

  
  

# ------------------------------------------------------------

# Hyperparameters

# ------------------------------------------------------------

batch_size = 128

epochs = 10

learning_rate = 1e-3

  

input_dim = 28 * 28 # MNIST image flattened size

hidden_dim = 400

latent_dim = 20 # Size of latent vector z

  

beta_values = [1, 2, 4, 8] # Different beta values for demo

  

save_dir = "beta_vae_models"

os.makedirs(save_dir, exist_ok=True)

  
  

# ------------------------------------------------------------

# MNIST Dataset

# ------------------------------------------------------------

transform = transforms.ToTensor()

  

train_dataset = datasets.MNIST(

root="./data",

train=True,

transform=transform,

download=True

)

  

train_loader = DataLoader(

train_dataset,

batch_size=batch_size,

shuffle=True

)

  
  

# ============================================================

# Beta-VAE Model

# ============================================================

class BetaVAE(nn.Module):

def __init__(self, input_dim, hidden_dim, latent_dim):

super(BetaVAE, self).__init__()

  

# ---------------- Encoder ----------------

# Input image x -> hidden representation

self.fc1 = nn.Linear(input_dim, hidden_dim)

  

# Encoder outputs mean and log-variance

self.fc_mu = nn.Linear(hidden_dim, latent_dim)

self.fc_logvar = nn.Linear(hidden_dim, latent_dim)

  

# ---------------- Decoder ----------------

# Latent vector z -> hidden representation

self.fc_dec1 = nn.Linear(latent_dim, hidden_dim)

  

# Hidden representation -> reconstructed image

self.fc_dec2 = nn.Linear(hidden_dim, input_dim)

  

def encode(self, x):

"""

Encoder:

Takes flattened image x and produces mu and logvar.

"""

h = F.relu(self.fc1(x))

mu = self.fc_mu(h)

logvar = self.fc_logvar(h)

return mu, logvar

  

def reparameterize(self, mu, logvar):

"""

Reparameterization trick:

  

z = mu + std * epsilon

  

This allows backpropagation through random sampling.

"""

std = torch.exp(0.5 * logvar)

epsilon = torch.randn_like(std)

z = mu + std * epsilon

return z

  

def decode(self, z):

"""

Decoder:

Takes latent vector z and reconstructs image.

"""

h = F.relu(self.fc_dec1(z))

  

# Sigmoid is used because MNIST pixel values are in [0, 1]

x_recon = torch.sigmoid(self.fc_dec2(h))

return x_recon

  

def forward(self, x):

"""

Full VAE forward pass:

x -> encoder -> mu, logvar -> z -> decoder -> reconstruction

"""

mu, logvar = self.encode(x)

z = self.reparameterize(mu, logvar)

x_recon = self.decode(z)

return x_recon, mu, logvar

  
  

# ============================================================

# Loss Function

# ============================================================

def beta_vae_loss(x_recon, x, mu, logvar, beta):

"""

Beta-VAE loss:

  

Total Loss = Reconstruction Loss + beta * KL Divergence

  

Reconstruction Loss:

Measures how close reconstructed image is to original image.

  

KL Divergence:

Forces latent distribution to remain close to standard normal N(0, I).

  

Beta:

Controls strength of KL regularization.

"""

  

# Binary cross entropy reconstruction loss

recon_loss = F.binary_cross_entropy(

x_recon,

x,

reduction="sum"

)

  

# KL divergence between q(z|x) and N(0, I)

kl_loss = -0.5 * torch.sum(

1 + logvar - mu.pow(2) - logvar.exp()

)

  

total_loss = recon_loss + beta * kl_loss

  

return total_loss, recon_loss, kl_loss

  
  

# ============================================================

# Training Loop

# ============================================================

def train_model(beta):

print(f"\nTraining Beta-VAE with beta = {beta}")

  

model = BetaVAE(input_dim, hidden_dim, latent_dim).to(device)

optimizer = torch.optim.Adam(model.parameters(), lr=learning_rate)

  

for epoch in range(epochs):

model.train()

  

total_loss = 0

total_recon_loss = 0

total_kl_loss = 0

  

for images, _ in train_loader:

# Flatten images from [B, 1, 28, 28] to [B, 784]

images = images.view(images.size(0), -1).to(device)

  

# Forward pass

recon_images, mu, logvar = model(images)

  

# Compute loss

loss, recon_loss, kl_loss = beta_vae_loss(

recon_images,

images,

mu,

logvar,

beta

)

  

# Backpropagation

optimizer.zero_grad()

loss.backward()

optimizer.step()

  

total_loss += loss.item()

total_recon_loss += recon_loss.item()

total_kl_loss += kl_loss.item()

  

avg_loss = total_loss / len(train_dataset)

avg_recon = total_recon_loss / len(train_dataset)

avg_kl = total_kl_loss / len(train_dataset)

  

print(

f"Epoch [{epoch+1}/{epochs}] "

f"Loss: {avg_loss:.4f} | "

f"Recon: {avg_recon:.4f} | "

f"KL: {avg_kl:.4f}"

)

  

# Save model

model_path = f"{save_dir}/beta_vae_beta_{beta}.pth"

torch.save(model.state_dict(), model_path)

print(f"Model saved at: {model_path}")

  
  

# ============================================================

# Train for multiple beta values

# ============================================================

for beta in beta_values:

train_model(beta)
```

### Generation with VAE

```python
# ============================================================

# Generate MNIST-like digits using trained Beta-VAE

# ============================================================

  

import torch

import torch.nn as nn

import torch.nn.functional as F

import matplotlib.pyplot as plt

  
  

# ------------------------------------------------------------

# Device setup

# ------------------------------------------------------------

device = torch.device("cuda" if torch.cuda.is_available() else "cpu")

  
  

# ------------------------------------------------------------

# Same model settings used during training

# ------------------------------------------------------------

input_dim = 28 * 28

hidden_dim = 400

latent_dim = 20

  

beta = 4 # Choose which trained beta model to load

model_path = f"beta_vae_models/beta_vae_beta_{beta}.pth"

  
  

# ============================================================

# Same Beta-VAE model definition

# ============================================================

class BetaVAE(nn.Module):

def __init__(self, input_dim, hidden_dim, latent_dim):

super(BetaVAE, self).__init__()

  

self.fc1 = nn.Linear(input_dim, hidden_dim)

self.fc_mu = nn.Linear(hidden_dim, latent_dim)

self.fc_logvar = nn.Linear(hidden_dim, latent_dim)

  

self.fc_dec1 = nn.Linear(latent_dim, hidden_dim)

self.fc_dec2 = nn.Linear(hidden_dim, input_dim)

  

def encode(self, x):

h = F.relu(self.fc1(x))

mu = self.fc_mu(h)

logvar = self.fc_logvar(h)

return mu, logvar

  

def reparameterize(self, mu, logvar):

std = torch.exp(0.5 * logvar)

epsilon = torch.randn_like(std)

z = mu + std * epsilon

return z

  

def decode(self, z):

h = F.relu(self.fc_dec1(z))

x_recon = torch.sigmoid(self.fc_dec2(h))

return x_recon

  

def forward(self, x):

mu, logvar = self.encode(x)

z = self.reparameterize(mu, logvar)

x_recon = self.decode(z)

return x_recon, mu, logvar

  
  

# ------------------------------------------------------------

# Load trained model

# ------------------------------------------------------------

model = BetaVAE(input_dim, hidden_dim, latent_dim).to(device)

model.load_state_dict(torch.load(model_path, map_location=device))

model.eval()

  

print(f"Loaded model from: {model_path}")

  
  

# ============================================================

# Generate new samples

# ============================================================

num_samples = 16

  

with torch.no_grad():

# Sample z from standard normal distribution N(0, I)

z = torch.randn(num_samples, latent_dim).to(device)

  

# Decode z to generate images

generated_images = model.decode(z)

  

# Reshape from [B, 784] to [B, 1, 28, 28]

generated_images = generated_images.view(num_samples, 1, 28, 28)

  
  

# ============================================================

# Display generated images

# ============================================================

plt.figure(figsize=(6, 6))

  

for i in range(num_samples):

plt.subplot(4, 4, i + 1)

plt.imshow(generated_images[i].cpu().squeeze(), cmap="gray")

plt.axis("off")

  

plt.suptitle(f"Generated MNIST Images using Beta-VAE, beta={beta}")

plt.tight_layout()

plt.show()
```