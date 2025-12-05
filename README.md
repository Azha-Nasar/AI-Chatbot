# 🤖 AI Chatbot

A neural network-powered conversational AI chatbot built with PyTorch and Flask, featuring intent classification, natural language processing, and a RESTful API for seamless integration into web and mobile applications.

## ✨ Features

### Core Capabilities
- **Intent Classification** - Accurately identifies user intents using a custom neural network
- **Natural Language Processing** - Tokenization and stemming with NLTK for better understanding
- **Confidence-Based Responses** - 75% confidence threshold ensures accurate replies
- **RESTful API** - Easy integration with any frontend application
- **Real-time Inference** - Fast response generation with GPU acceleration support
- **Fallback Handling** - Graceful responses for unrecognized queries

### Supported Intents
- **Greetings** - Friendly welcome messages and casual conversation
- **Farewells** - Polite goodbye responses
- **Gratitude** - Acknowledgment of thanks and appreciation
- **Balance Inquiry** - Check account balance ($4,200 demo data)
- **Money Transfer** - Initiate fund transfer requests
- **Unknown** - Fallback responses for unclear queries

### API Features
- **CORS Enabled** - Cross-origin requests supported for frontend integration
- **JSON Response Format** - Standardized API responses
- **POST Endpoint** - Simple message-response interface
- **Error Handling** - Robust error management

## 🛠️ Technology Stack

- **Deep Learning**: PyTorch (Neural Network Framework)
- **NLP**: NLTK (Tokenization, Stemming, Bag-of-Words)
- **Backend**: Flask (RESTful API)
- **Data Processing**: NumPy
- **Cross-Origin Support**: Flask-CORS

## 📋 Prerequisites

- Python 3.7 or higher
- pip (Python package manager)
- Virtual environment (recommended)
- GPU with CUDA support (optional, for faster training)

## 🚀 Installation

### 1. Clone the Repository

```bash
git clone https://github.com/yourusername/AI-Chatbot.git
cd AI-Chatbot
```

### 2. Create Virtual Environment (Recommended)

```bash
# Windows
python -m venv venv
venv\Scripts\activate

# macOS/Linux
python3 -m venv venv
source venv/bin/activate
```

### 3. Install Dependencies

```bash
pip install torch numpy nltk flask flask-cors
```

### 4. Download NLTK Data

```bash
python -c "import nltk; nltk.download('punkt')"
```

Or run:
```python
import nltk
nltk.download('punkt')
```

### 5. Train the Model

```bash
python train.py
```

Expected output:
```
44 patterns
6 tags: ['balance', 'goodbye', 'greeting', 'thanks', 'transfer', 'unknown']
45 unique stemmed words: [...]
Epoch [100/1000], Loss: 0.4521
Epoch [200/1000], Loss: 0.1234
...
Final Loss: 0.0156
Training complete. File saved to data.pth
```

### 6. Start the Server

```bash
python app.py
```

Server will start at `http://localhost:5000`

## 🎯 Usage

### API Endpoint

**POST** `/predict`

**Request Body:**
```json
{
  "message": "Hello, how are you?"
}
```

**Response:**
```json
{
  "answer": "Hi there!"
}
```

### Example Using cURL

```bash
curl -X POST http://localhost:5000/predict \
  -H "Content-Type: application/json" \
  -d '{"message": "What is my balance?"}'
```

### Example Using Python

```python
import requests

url = "http://localhost:5000/predict"
data = {"message": "Hello!"}

response = requests.post(url, json=data)
print(response.json())  # {'answer': 'Greetings!'}
```

### Example Using JavaScript (Fetch API)

```javascript
fetch('http://localhost:5000/predict', {
  method: 'POST',
  headers: {
    'Content-Type': 'application/json',
  },
  body: JSON.stringify({ message: 'Hi there!' })
})
  .then(response => response.json())
  .then(data => console.log(data.answer));
```

## 📁 Project Structure

```
AI-Chatbot/
├── app.py                  # Flask API server
├── chat.py                 # Response generation logic
├── train.py                # Model training script
├── model.py                # Neural network architecture
├── nltk_utils.py           # NLP utilities
├── intents.json            # Training data & responses
├── data.pth                # Trained model (generated)
├── README.md               # Documentation
└── requirements.txt        # Dependencies (optional)
```

## 🧠 Neural Network Architecture

```
Input Layer (Bag of Words)
         ↓
Hidden Layer 1 (8 neurons) + ReLU
         ↓
Hidden Layer 2 (8 neurons) + ReLU
         ↓
Output Layer (Intent Classes)
         ↓
Softmax Activation
```

**Hyperparameters:**
- Input Size: 45 (vocabulary size)
- Hidden Size: 8 neurons
- Output Size: 6 (number of intents)
- Learning Rate: 0.001
- Epochs: 1000
- Batch Size: 8
- Optimizer: Adam

## 🎨 Customization

### Adding New Intents

Edit `intents.json`:

```json
{
  "tag": "hours",
  "patterns": [
    "What are your hours?",
    "When are you open?",
    "Business hours",
    "Are you open now?",
    "Working hours"
  ],
  "responses": [
    "We're open 24/7!",
    "Our service is available around the clock.",
    "We're always here to help!"
  ]
}
```

**Then retrain:**
```bash
python train.py
```

### Modifying Training Parameters

In `train.py`:

```python
# Increase hidden layer neurons for complex patterns
hidden_size = 16  # Default: 8

# Adjust learning rate
learning_rate = 0.0005  # Default: 0.001

# Extend training duration
num_epochs = 2000  # Default: 1000

# Change batch size
batch_size = 16  # Default: 8
```

### Adjusting Confidence Threshold

In `chat.py`:

```python
# Lower threshold for more responses (may reduce accuracy)
if prob.item() > 0.65:  # Default: 0.75
    return random.choice(intent["responses"])
```

### Custom Fallback Message

In `chat.py`:

```python
return "I'm not sure I understand. Could you please rephrase?"
# Change to your custom message
```

## 📊 Model Performance

| Metric | Value |
|--------|-------|
| Training Loss | ~0.015 |
| Confidence Threshold | 75% |
| Response Time | <100ms |
| Vocabulary Size | 45 words |
| Intent Classes | 6 |

## 🔐 Security Considerations

- Input validation required for production use
- Rate limiting recommended for API endpoint
- Authentication/authorization not included (add as needed)
- No sensitive data stored in model
- CORS is open (restrict in production)

## 🐛 Troubleshooting

### Common Issues

**Issue: NLTK punkt not found**
```bash
python -c "import nltk; nltk.download('punkt')"
```

**Issue: Module not found**
```bash
pip install -r requirements.txt
```

**Issue: CORS errors**
- Ensure Flask-CORS is installed
- Check frontend URL configuration

**Issue: Low accuracy responses**
- Add more training patterns
- Increase hidden_size
- Train for more epochs
- Check confidence threshold

**Issue: Model file not found**
- Run `python train.py` first
- Check `data.pth` exists in directory

## 🔄 Future Enhancements

- [ ] Multi-turn conversation support with context memory
- [ ] Entity extraction (names, dates, amounts)
- [ ] Integration with external APIs (weather, news)
- [ ] Multilingual support
- [ ] Voice input/output capability
- [ ] Sentiment analysis
- [ ] User authentication and personalization
- [ ] Conversation history storage
- [ ] Admin dashboard for analytics
- [ ] Docker containerization
- [ ] Cloud deployment (AWS, Azure, GCP)
- [ ] Webhook integration for notifications

## 📈 Performance Optimization

### For Training
- Use GPU acceleration with CUDA
- Increase batch size for faster training
- Use learning rate scheduling

### For Inference
- Cache common responses
- Use model quantization
- Implement request batching
- Deploy with production WSGI server (Gunicorn, uWSGI)

## 🤝 Contributing

Contributions are welcome! Please follow these steps:

1. Fork the repository
2. Create a feature branch (`git checkout -b feature/AmazingFeature`)
3. Commit your changes (`git commit -m 'Add some AmazingFeature'`)
4. Push to the branch (`git push origin feature/AmazingFeature`)
5. Open a Pull Request

### Contribution Guidelines
- Follow PEP 8 style guide
- Add tests for new features
- Update documentation
- Keep commits atomic and descriptive

## 👥 Author

Azha Nasar

## 📧 Contact

For questions or support, please contact:
- Email: azhanasar03@gmail.com
- Linkedin Profile : https://www.linkedin.com/in/azha-nasar-3a7ba2330
- Project Link: [https://github.com/Azha-Nasar/AI-Chatbot](https://github.com/Azha-Nasar/AI-Chatbot)

## 📝 License

This project is licensed under the MIT License - see the [LICENSE](LICENSE) file for details.

## 🙏 Acknowledgments

- PyTorch team for the deep learning framework
- NLTK developers for NLP tools
- Flask community for the web framework
- Open source contributors

## 📚 Resources

- [PyTorch Documentation](https://pytorch.org/docs/)
- [NLTK Documentation](https://www.nltk.org/)
- [Flask Documentation](https://flask.palletsprojects.com/)
- [Neural Networks Tutorial](https://pytorch.org/tutorials/beginner/blitz/neural_networks_tutorial.html)

---

**⭐ If you found this project helpful, please give it a star!**

**Made with ❤️ and PyTorch**
