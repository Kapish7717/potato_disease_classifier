# Potato Disease Detection System

**Technologies:** Python, TensorFlow, FastAPI, Docker

A deep learning application to detect and classify potato leaf diseases (Early Blight, Late Blight, Healthy) using a custom CNN model, served via TensorFlow Serving and accessible through a FastAPI API.

---

## Features

* Custom CNN model trained from scratch for potato leaf disease classification.
* Image preprocessing and data augmentation for robust predictions.
* Achieved **90%+ accuracy** on test data.
* Real-time inference through FastAPI endpoint.
* Deployment using **TensorFlow Serving** inside Docker for portability.

---

## Folder Structure

```
potato-disease-classifier/
│
├── app/                  # FastAPI application
│   └── main.py
│
├── models/               # Trained model directory
│   └── my_model/
│       └── 1/
│           ├── saved_model.pb
│           └── variables/
│
├── Docker/               # Docker setup files
│   └── Dockerfile
│
├── requirements.txt      # Python dependencies
├── models.config         # TensorFlow Serving config
└── README.md             # Project documentation
```

---

## Installation

1. **Clone the repository**

```bash
git clone https://github.com/Kapish7717/potato_disease_classifier.git
cd potato_disease_classifier
```

2. **Install dependencies**

```bash
pip install -r requirements.txt
```

3. **Run FastAPI**

```bash
uvicorn app.main:app --reload
```

4. **Start TensorFlow Serving (Docker)**

```bash
docker run -t --rm -p 8501:8501 \
  -v "${PWD}/models:/models/my_model" \
  -v "${PWD}/models.config:/models/models.config" \
  tensorflow/serving \
  --model_config_file=/models/models.config
```

---

## Usage

### Predict via API

Send a POST request to the FastAPI endpoint:

```bash
curl -X POST http://localhost:8000/predict \
     -F "file=@leaf_image.jpg"
```

**Response example:**

```json
{
  "predictions": [
    {
      "predicted_class": "Early Blight",
      "confidence": 0.95
    }
  ]
}
```

---

## Acknowledgements

* TensorFlow documentation: [https://www.tensorflow.org/](https://www.tensorflow.org/)
* FastAPI documentation: [https://fastapi.tiangolo.com/](https://fastapi.tiangolo.com/)
