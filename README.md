# AI-Chatbot

A neural network-based chatbot built with PyTorch and Flask that can understand and respond to various user intents like greetings, account balance inquiries, and money transfers.

## Features

- Intent classification using a custom neural network
- Natural language processing with NLTK
- RESTful API built with Flask
- Pre-trained model for quick deployment
- Extensible intent system

## Architecture

The chatbot uses a feed-forward neural network with:
- Input layer: Bag-of-words representation
- Two hidden layers with ReLU activation
- Output layer: Intent classification
- Confidence threshold: 75% for responses

## Installation

### Prerequisites

- Python 3.7+
- pip

### Setup

1. Clone the repository:
```bash
git clone <repository-url>
cd AI-Chatbot
```

2. Install required packages:
```bash
pip install torch numpy nltk flask flask-cors
```

3. Download NLTK data:
```python
python -c "import nltk; nltk.download('punkt')"
```

## Usage

### Training the Model

To train the chatbot with your intents:

```bash
python train.py
```

This will:
- Process patterns from `intents.json`
- Train the neural network
- Save the trained model to `data.pth`

### Running the Server

Start the Flask API server:

```bash
python app.py
```

The server will run on `http://localhost:5000` by default.

### Making Requests

Send POST requests to `/predict` endpoint:

```bash
curl -X POST http://localhost:5000/predict \
  -H "Content-Type: application/json" \
  -d '{"message": "Hello"}'
```

Response:
```json
{
  "answer": "Hi there!"
}
```

## Project Structure

```
AI-Chatbot/
├── app.py              # Flask API server
├── chat.py             # Chatbot logic and response generation
├── train.py            # Model training script
├── model.py            # Neural network architecture
├── nltk_utils.py       # NLP utilities (tokenization, stemming)
├── intents.json        # Training data and response templates
├── data.pth            # Trained model (generated after training)
└── README.md           # Project documentation
```

## Customization

### Adding New Intents

Edit `intents.json` to add new conversation patterns:

```json
{
  "tag": "hours",
  "patterns": [
    "What are your hours?",
    "When are you open?",
    "Business hours"
  ],
  "responses": [
    "We're open 24/7!",
    "Our service is available around the clock."
  ]
}
```

After modifying intents, retrain the model:

```bash
python train.py
```

### Adjusting Model Parameters

In `train.py`, you can modify:
- `hidden_size`: Number of neurons in hidden layers (default: 8)
- `learning_rate`: Training learning rate (default: 0.001)
- `num_epochs`: Number of training iterations (default: 1000)
- `batch_size`: Training batch size (default: 8)

### Confidence Threshold

In `chat.py`, adjust the confidence threshold (default: 0.75):

```python
if prob.item() > 0.75:  # Change this value
```

## Current Intents

- **greeting**: Casual greetings and hellos
- **goodbye**: Farewells and departure messages
- **thanks**: Expressions of gratitude
- **balance**: Account balance inquiries
- **transfer**: Money transfer requests
- **unknown**: Fallback for unrecognized inputs

## API Reference

### POST /predict

Processes a user message and returns a chatbot response.

**Request Body:**
```json
{
  "message": "string"
}
```

**Response:**
```json
{
  "answer": "string"
}
```

## Dependencies

- **torch**: Neural network framework
- **numpy**: Numerical computations
- **nltk**: Natural language processing
- **flask**: Web framework
- **flask-cors**: Cross-origin resource sharing

## Notes

- The model requires retraining after any changes to `intents.json`
- CUDA GPU support is automatically enabled if available
- Responses are randomly selected from the intent's response list
- The chatbot returns a fallback message for inputs below the confidence threshold

## Future Improvements

- Add conversation context/memory
- Implement entity extraction
- Support for multi-turn dialogues
- Integration with external APIs
- User authentication and session management
