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
│ ├── Training_model_extend.ipynb # Autoencoder trained on MNIST
│ └── vae_model.pt # Saved model weights
│
├── Kaggle Autoencoder/
│ ├── kaggle_Auto_encoder (2).ipynb # Autoencoder for Intel dataset
│ └── lora_autoencoder (2).pt # Saved model weights
│
├── New Improved MNIST VAE model/
│ ├── New_VAE_Model.ipynb # Enhanced VAE training
│ └── vae_model_improved.pth # Improved model weights
| |__ New_VAE_Model.ipynb  # Extended version of the improved VAE notebook, includes full test pipeline.
```
 
---
 
## Datasets
 
| Dataset | Images | Size | Purpose |
|---|---|---|---|
| MNIST | 70,000 | 28×28 greyscale | Baseline | Divide packets x 3 | 
| Intel Image Classification (Kaggle) | ~25,000 | 240×320 RGB | Real-world test |
| Improved MNIST | 70,000 | 28×28 greyscale | Baseline | Divide packets x 6 |
 
---
 
## Model
 
### LoRaAutoEncoder (Kaggle)
- 3-layer convolutional encoder/decoder  
- Input: `(3, 240, 320)` RGB image  
- Latent: `[16, 30, 40]` = 19,200 values  
- Loss: MSE reconstruction loss  

### MNIST VAE
- Designed for grayscale image compression  
- Lightweight and fast baseline model  

### New Improved MNIST VAE
- Enhanced VAE architecture  
- Latent size: 64  
- Designed for:
  - Improved compression efficiency  
  - Better reconstruction quality  
  - Robustness to packet loss  

**Functionality:**
- Encodes image into latent vector  
- Splits into 6 LoRa packets  
- Handles missing packets during reconstruction  
- Produces more stable outputs under packet loss  

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
 
### Improved MNIST VAE
| Condition | SSIM |
|---|---|
| No packet loss | ~0.9+ |
| 1 packet loss | Slight drop |
| 2 packet loss | Moderate drop |
| 3 packet loss | Significant drop |
 
> LoRa packet size: ~48–51 bytes | 6 packets per image
 
---
 
## Tools & Libraries
 
- Python, PyTorch, Google Colab  
- NumPy, PIL  
- `scikit-image` (SSIM), `torchvision`  
- Raspberry Pi + LoRa modules (RFM9x)  
- INA219 power sensor (energy measurement)  
 
---
---
 
## Tools & Libraries
 
- Python, PyTorch, Google Colab
- `scikit-image` (SSIM), `torchvision`
- Raspberry Pi + LoRa modules (hardware phase)
 
---
