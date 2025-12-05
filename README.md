📱 Android Malware Detection Using Federated Learning (FL)

This repository contains the implementation of a privacy-preserving Android malware detection framework using Federated Learning (FL).
The project uses a multimodal feature set (permissions, intents, hardware features) and simulates 5 clients training a lightweight neural network on non-IID data using the Flower (FLWR) framework.

The global model achieves 96.41% accuracy while ensuring zero raw-data sharing across clients.

🔥 Key Features

Federated Learning (FL) implementation using FLWR

Multimodal feature extraction

Permissions

Intents

Hardware Features

One-Hot Encoding for all categorical app features

Non-IID dataset simulation across 5 clients

Local training + FedAvg aggregation

Lightweight, fully connected neural network (TensorFlow/Keras)

Privacy-preserving architecture (only model weights shared)

Achieved 96.41% global accuracy in 15 rounds

🏗️ System Architecture
          ┌──────────────┐
          │   Server      │
          │ (FedAvg)      │
          └──────┬────────┘
                 │
   ┌─────────────┼──────────────────┐
   │             │                  │
┌─────┐     ┌─────┐           ┌─────┐
│Client│     │Client│           │Client│   ... (5 total)
│  1   │     │  2    │           │  3    │
└─────┘     └──────┘           └──────┘
 Local Training → Send Weights → Aggregate → Broadcast

🧬 Dataset & Features

The dataset includes benign + malware Android apps.
Static features extracted:

Category	Examples
Permissions	CAMERA, READ_CONTACTS, INTERNET, etc.
Intents	BOOT_COMPLETED, SEND, VIEW, etc.
Hardware	GPS, NFC, Bluetooth, Accelerometer

All features are converted using One-Hot Encoding, then merged into a single high-dimensional feature vector.

🚀 How to Run
1️⃣ Install Requirements
pip install -r requirements.txt

2️⃣ Prepare Dataset

Place the processed dataset in:

/data/
    merged_features.csv

3️⃣ Run the Server
python server.py

4️⃣ Run the Clients (in 5 terminals)
python client.py --client_id=1
python client.py --client_id=2
...
python client.py --client_id=5

🧠 Model Architecture (Local Client)
Input Layer (merged multimodal features)
↓
Dense (128) + ReLU
↓
Dropout (0.3)
↓
Dense (64) + ReLU
↓
Dense (1) + Sigmoid   # malware / benign


Loss: Binary Cross-Entropy

Optimizer: Adam

Batch size: 64

Local epochs: 10

Federated rounds: 15

📊 Results
Metric	Score
Accuracy	96.41%
Loss	0.036
Rounds	15
Clients	5 (non-IID)

FL successfully preserved user privacy without any loss of detection performance.

📄 Paper

This implementation corresponds to the research paper:

Android Malware Detection Using Federated Learning
