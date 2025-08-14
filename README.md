# Disease Detection ML Backend

A comprehensive machine learning backend for disease prediction based on symptoms. This application uses multiple ML algorithms to predict diseases and provides precautionary measures.

## Features

- **Multiple ML Models**: Random Forest, SVM, Naive Bayes, Logistic Regression, Gradient Boosting, and K-Nearest Neighbors
- **RESTful API**: Clean and well-documented API endpoints
- **Model Performance Metrics**: Accuracy, Precision, Recall, F1-Score, and Cross-validation scores
- **Symptom Preprocessing**: Intelligent symptom matching and normalization
- **Disease Precautions**: Provides precautionary measures for predicted diseases
- **Model Persistence**: Save and load trained models
- **Comprehensive Logging**: Detailed logging for monitoring and debugging

## Dataset

The application uses two CSV files:
- `DiseaseAndSymptoms.csv`: Contains diseases and their associated symptoms
- `Disease precaution.csv`: Contains precautionary measures for each disease

## Installation

1. Install Python dependencies:
```bash
pip install -r requirements.txt
```

2. Ensure your data files are in the `data/` directory:
   - `data/DiseaseAndSymptoms.csv`
   - `data/Disease precaution.csv`

3. Run the application:
```bash
python app.py
```

The API will be available at `http://localhost:5000`

## API Endpoints

### Health Check
```
GET /health
```
Returns the health status of the API.

### Train Models
```
POST /train-models
```
Trains all ML models and returns performance metrics.

### Predict Disease
```
POST /predict
Content-Type: application/json

{
    "symptoms": ["fever", "cough", "headache", "fatigue"]
}
```
Predicts diseases based on provided symptoms.

### Get Available Symptoms
```
GET /available-symptoms
```
Returns a list of all available symptoms in the dataset.

### Get Available Diseases
```
GET /diseases
```
Returns a list of all diseases that can be predicted.

### Get Model Performance
```
GET /model-performance
```
Returns performance metrics for all trained models.

## Usage Example

1. **Start the server:**
```bash
python app.py
```

2. **Train the models:**
```bash
curl -X POST http://localhost:5000/train-models
```

3. **Make a prediction:**
```bash
curl -X POST http://localhost:5000/predict \
  -H "Content-Type: application/json" \
  -d '{"symptoms": ["fever", "cough", "headache"]}'
```

## Testing

Run the test script to verify all endpoints:
```bash
python test_api.py
```

## Model Performance

The application trains multiple models and provides comprehensive metrics:

- **Accuracy**: Overall correctness of predictions
- **Precision**: Ratio of correctly predicted positive observations
- **Recall**: Ratio of correctly predicted positive observations to all observations
- **F1-Score**: Weighted average of Precision and Recall
- **Cross-Validation**: 5-fold cross-validation accuracy

## Architecture

```
├── app.py                 # Main Flask application
├── ml_models.py          # ML model training and prediction logic
├── data_preprocessing.py # Data preprocessing and symptom matching
├── utils.py              # Utility functions
├── config.py             # Configuration settings
├── test_api.py           # API testing script
├── requirements.txt      # Python dependencies
└── data/                 # Dataset directory
    ├── DiseaseAndSymptoms.csv
    └── Disease precaution.csv
```

## Key Features

### Intelligent Symptom Matching
- Normalizes user input symptoms
- Matches symptoms using exact, partial, and word-based matching
- Handles variations in symptom descriptions

### Multiple ML Models
- Ensemble approach using 6 different algorithms
- Model comparison and performance evaluation
- Confidence scores for predictions

### Comprehensive Error Handling
- Input validation
- Graceful error responses
- Detailed logging

### Model Persistence
- Automatic model saving after training
- Model loading on application startup
- Efficient prediction without retraining

## Configuration

Environment variables can be set in a `.env` file:

```env
FLASK_DEBUG=True
SECRET_KEY=your-secret-key
SYMPTOMS_DATA_PATH=data/DiseaseAndSymptoms.csv
PRECAUTIONS_DATA_PATH=data/Disease precaution.csv
AUTO_TRAIN_ON_STARTUP=True
MAX_SYMPTOMS_PER_REQUEST=20
CV_FOLDS=5
TEST_SIZE=0.2
RANDOM_STATE=42
```

## Production Deployment

For production deployment:

1. Set `FLASK_DEBUG=False`
2. Use a production WSGI server like Gunicorn:
```bash
gunicorn -w 4 -b 0.0.0.0:5000 app:app
```

## Contributing

1. Fork the repository
2. Create a feature branch
3. Make your changes
4. Add tests
5. Submit a pull request

## License

This project is licensed under the MIT License.

## Disclaimer

This application is for educational and informational purposes only. It should not be used as a substitute for professional medical advice, diagnosis, or treatment. Always consult with a qualified healthcare provider for medical concerns.