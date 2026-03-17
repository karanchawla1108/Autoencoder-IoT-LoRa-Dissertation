# Autoencoder-IoT-LoRa-Dissertation
 
Final year dissertation — BSc (Hons) Computer Science, York St John University (2025–26)
 
---
 
## What This Project Does
 
Compresses images using a trained Autoencoder, then simulates sending the compressed data over a **LoRa** (Low Power Wide Area) radio network. The goal is to find out how well images survive LoRa's tiny bandwidth and packet loss.
 
```
Image → Encoder → Latent Vector → LoRa Packets → Decoder → Reconstructed Image
```
 
---
 
## Repo Structure
 
```
Autoencoder-IoT-LoRa-Dissertation/
├── MNIST Autoencoder/
│   ├── Training_model_extend.ipynb   # VAE trained on MNIST digits
│   └── vae_model.pt                  # Saved model weights
│
└── Kaggle Autoencoder/
    ├── kaggle_Auto_encoder (2).ipynb    # Autoencoder trained on Intel dataset
    └── lora_autoencoder (2).pt          # Saved model weight
```
 
---
 
## Datasets
 
| Dataset | Images | Size | Purpose |
|---|---|---|---|
| MNIST | 70,000 | 28×28 greyscale | Baseline |
| Intel Image Classification (Kaggle) | ~25,000 | 240×320 RGB | Real-world test |
 
---
 
## Model
 
**LoRaAutoEncoder** — 3-layer convolutional encoder/decoder
 
- Input: `(3, 240, 320)` RGB image
- Latent: `[16, 30, 40]` = 19,200 values
- Loss: MSE reconstruction loss
 
---
 
## Results
 
### MNIST (VAE)
| Condition | SSIM |
|---|---|
| No packet loss | 0.8480 |
| 20% packet loss | 0.6395 |
 
### Intel / Kaggle (Autoencoder)
| Packet Loss | SSIM |
|---|---|
| 0% | 0.63 |
| 10% | 0.30 |
| 20% | 0.21 |
| 30% | 0.17 |
| 40% | 0.14 |
 
> LoRa packet size: 51 bytes | ~376 packets per image
 
---
 
## Tools & Libraries
 
- Python, PyTorch, Google Colab
- `scikit-image` (SSIM), `torchvision`
- Raspberry Pi + LoRa modules (hardware phase)
 
---
