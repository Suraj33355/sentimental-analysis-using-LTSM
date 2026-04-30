# Sentiment Analysis Web Application

A Flask-based web application that performs sentiment analysis on text using a pre-trained deep learning model. Analyze single texts or batch process CSV files with sentiment predictions and visualizations.

## Features

- **Single Text Analysis**: Enter any text and get instant sentiment prediction (Positive/Negative/Neutral) with confidence score
- **Batch CSV Processing**: Upload CSV files to analyze multiple texts at once and generate sentiment distribution visualizations
- **Deep Learning Model**: Uses a trained Keras LSTM neural network for accurate sentiment classification
- **Interactive UI**: Modern animated web interface with responsive design
- **Real-time Results**: Quick sentiment predictions with elapsed time tracking
- **Visual Feedback**: Emoji-based sentiment indicators (😊 Happy, 😐 Neutral, 😞 Sad)

## Project Structure

```
Sentiment Analysis/
├── app.py                      # Flask web server & main application logic
├── SetimentAnalysis.py         # Sentiment analysis utilities & helper functions
├── SentimentAnalysis.ipynb     # Jupyter notebook with model training & analysis
├── model.h5                    # Pre-trained Keras LSTM model
├── tokenizer.pkl               # Fitted tokenizer for text preprocessing
├── templates/
│   ├── index.html              # Main landing page with input forms
│   ├── suraj2.html             # Results page displaying predictions
│   └── suraj3.html             # Additional template
├── static/
│   ├── Happy_Emoji.webp        # Positive sentiment emoji
│   ├── Neutral-Face.png        # Neutral sentiment emoji
│   ├── Sad_Emoji.png           # Negative sentiment emoji
│   ├── suraj.jpg               # UI image
│   ├── abhi.png                # UI image
│   ├── suri.png                # UI image
│   └── Graph.png               # Sample visualization
└── README.md                   # This file
```

## Installation

### Prerequisites
- Python 3.7 or higher
- pip (Python package manager)

### Setup

1. **Clone or download the project**
   ```bash
   cd "Sentimental Analysis"
   ```

2. **Install required dependencies**
   ```bash
   pip install -r requirements.txt
   ```
   
   Or install manually:
   ```bash
   pip install flask keras tensorflow pandas matplotlib
   ```

3. **Ensure model files are present**
   - `model.h5` - Pre-trained sentiment model
   - `tokenizer.pkl` - Text tokenizer

## Usage

### Running the Application

```bash
python app.py
```

The application will start on `http://localhost:5000`

### Analyzing Text

1. Open the web application in your browser
2. Enter text in the "Enter Text Here" section
3. Click **Submit**
4. View the sentiment prediction with confidence score and emoji indicator

### Batch Processing CSV

1. Open the web application
2. In the "Choose CSV File" section, select a CSV file with a "Text" column
3. Click **Import**
4. The application will:
   - Analyze sentiment for each text entry
   - Generate a sentiment distribution chart
   - Display results

## How It Works

### Sentiment Classification

The model classifies text into three categories based on prediction score:

| Score Range | Sentiment | Indicator |
|-------------|-----------|-----------|
| ≤ 0.4 | Negative | 😞 |
| 0.4 - 0.7 | Neutral | 😐 |
| ≥ 0.7 | Positive | 😊 |

### Text Processing Pipeline

1. **Input**: Raw text or CSV data
2. **Tokenization**: Text converted to sequences using the fitted tokenizer
3. **Padding**: Sequences padded/truncated to 300 tokens
4. **Model Prediction**: LSTM neural network processes padded sequences
5. **Sentiment Decoding**: Raw score converted to sentiment label
6. **Output**: Label, confidence score, and processing time

## Model Details

- **Architecture**: Keras Sequential model with LSTM layers
- **Input Sequence Length**: 300 tokens (max)
- **Output**: Probability score (0-1) for sentiment
- **Training**: Callbacks include ReduceLROnPlateau and EarlyStopping

## API Endpoints

### GET /
Returns the main landing page with input forms.

**Response**: HTML page (index.html)

### POST /
Processes sentiment analysis request for either text or CSV file.

**Parameters:**
- **Text Input**: 
  - `text` (form parameter): Text to analyze
  - `login` (form parameter): Submission trigger

- **CSV Upload**:
  - `file` (form file): CSV file with "Text" column
  - `uploadCsv` (form name): Submission trigger

**Response**: Results page (suraj2.html) with sentiment prediction or CSV analysis results

## Dependencies

- **Flask**: Web framework for routing and serving templates
- **Keras/TensorFlow**: Deep learning model and predictions
- **Pandas**: CSV file handling and data manipulation
- **Matplotlib**: Visualization generation for batch results
- **Pickle**: Model and tokenizer serialization

## File Descriptions

### app.py
Main Flask application containing:
- Route handlers for GET and POST requests
- Text sentiment prediction logic
- CSV batch processing with visualization
- Error handling for file uploads

### SetimentAnalysis.py
Reusable sentiment analysis module with:
- `decode_sentiment()`: Converts prediction scores to labels
- `predict()`: Single text prediction with timing
- `predict_csv()`: CSV row prediction
- Model and tokenizer loading

### SentimentAnalysis.ipynb
Jupyter notebook documenting:
- Data loading and exploration
- Model training and evaluation
- Visualization and analysis
- 40+ computational cells

## Example CSV Format

Your CSV file should contain a "Text" column:

```csv
Text
"This product is amazing!"
"I don't like this at all."
"It's okay, nothing special."
```

## Performance Notes

- Single text analysis typically completes in < 1 second
- CSV batch processing depends on file size and system resources
- Model predictions include elapsed time in the output

## Troubleshooting

| Issue | Solution |
|-------|----------|
| Model not found | Ensure `model.h5` and `tokenizer.pkl` are in the project root |
| Port 5000 in use | Change Flask port in app.py or kill existing process |
| CSV file error | Verify CSV has "Text" column and proper formatting |
| Import errors | Run `pip install -r requirements.txt` to install all dependencies |

## Future Improvements

- Add support for multiple languages
- Implement model fine-tuning capability
- Add user authentication and result history
- Create API documentation with Swagger
- Add more sentiment categories (e.g., mixed sentiment)
- Implement confidence threshold filtering

## License

This project is provided as-is for educational and personal use.

## Author

Created as a sentiment analysis learning project.

---

**Last Updated**: April 2026
