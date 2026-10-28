# Moodline — Emotion Prediction

**An instrument that reads the mood inside a sentence.**

🔗 **Live Demo:** https://emotion-prediction-p3jt.onrender.com/

## About the Project

Moodline is a small machine learning web application that explores how emotions can be identified from written text.

The idea behind the project is simple: we express different emotions through everyday messages, but identifying the emotion behind a sentence isn't always straightforward. Moodline takes a sentence as input, processes it using a trained deep learning model, and predicts the emotion that best matches the text.

I built the application with a simple, focused interface. Instead of showing only a predicted label, it displays a confidence score and a breakdown of the predicted probabilities across different emotions.

For example, when a user enters *"omg today i got my first job"*, the application might identify **Joy** as the most likely emotion and show how the model distributes its predictions across other categories.

The goal is to make the prediction easy to explore while connecting a machine learning model to a usable web application.

## Try It Out

Open the live application:

**https://emotion-prediction-p3jt.onrender.com/**

Enter a sentence in the input area and click **Read the mood** to see the predicted emotion and its confidence score.

You can try different kinds of sentences, including messages that express happiness, sadness, fear, anger, surprise, or love.

## Features

### 1. Text-Based Emotion Prediction

Users can enter a sentence or short message, and Moodline predicts the emotion that best matches the text.

The application is designed for quick experiments with everyday language rather than long documents.

### 2. Six Emotion Categories

Moodline works with six emotion categories:

- 😄 **Joy** — happiness, excitement, or positive experiences
- 😢 **Sadness** — disappointment, grief, or feeling low
- 😨 **Fear** — worry, nervousness, or uncertainty
- 😠 **Anger** — frustration, irritation, or displeasure
- 😲 **Surprise** — unexpected or surprising experiences
- ❤️ **Love** — affection, care, or warm feelings

The categories represent the emotions the model is trained to recognize. Real sentences can express more than one emotion, so the model's prediction may not always match how a person interprets the message.

### 3. Confidence Score

After processing the text, the application displays the predicted emotion along with a confidence score.

For example, if the model returns Joy with a score of 80.9%, the interface presents that value as the model's confidence for its selected class.

This score should not be interpreted as a guarantee that the sentence expresses that emotion. Model confidence depends on the model, its training data, and the input text.

### 4. Emotion Breakdown

Moodline also displays the scores for the other emotion categories.

This makes it possible to compare the model's strongest prediction with its alternatives rather than looking at a single label.

For instance, a sentence might receive a high Joy score with smaller scores for Sadness or Fear.

### 5. Simple, Interactive Interface

The interface is designed to keep the main task straightforward:

- Enter a sentence.
- Analyze the text.
- View the predicted emotion.
- Compare the scores for all six categories.

The application also supports a keyboard shortcut for submitting text, making it convenient to test multiple sentences.

## Tech Stack

The project combines a Python machine learning backend with a lightweight web interface.

| Technology | Purpose |
|---|---|
| Python | Backend logic and model integration |
| TensorFlow / Keras | Loading and running the trained deep learning model |
| BiGRU | Bidirectional recurrent neural network architecture used by the model |
| NumPy | Numerical operations and prediction processing |
| FastAPI | Backend API and request handling |
| Uvicorn | Running the FastAPI application |
| HTML | Structure of the web interface |
| CSS | Layout, styling, and visual design |
| JavaScript | User interactions and communication with the backend |
| Render | Hosting the live application |

## How It Works

The application follows a simple flow from user input to prediction.

1. **Text input:** The user enters a sentence in the Moodline interface.
2. **Text preprocessing:** The input is prepared for the trained model using the project's text-processing pipeline.
3. **Tokenization:** The tokenizer converts words or tokens into the numerical representation expected by the model.
4. **Model inference:** The saved BiGRU model processes the input and produces scores for the emotion categories.
5. **Prediction selection:** The application selects the category with the highest output score.
6. **Result display:** The frontend displays the predicted emotion, confidence score, and emotion breakdown.

The tokenizer and trained model are important parts of the prediction pipeline. They need to remain compatible with each other for the application to produce meaningful results.

## Understanding the BiGRU Model

Moodline uses a trained BiGRU model for text classification.

A GRU (Gated Recurrent Unit) is a type of recurrent neural network designed to process sequential data. It uses gates to control how information is retained or updated as the sequence is processed.

A **Bidirectional GRU (BiGRU)** processes a text sequence in both forward and backward directions. This can help the model learn from context on both sides of a word when processing the full sequence.

For emotion prediction, context matters because the same word can have different meanings depending on the rest of the sentence.

For example, a sentence about getting a first job may express joy, while a sentence about losing a job may express sadness. The model uses patterns learned during training to distinguish between different classes.

The quality of the prediction depends on the training data, preprocessing, model configuration, and how closely the input resembles the text seen during training.

## Project Structure

The repository contains the main application, saved model artifacts, frontend files, and dependency configuration.

```text
Emotion-Prediction-main/
│
├── Artifacts/
│   ├── BiGRU_Model.keras
│   └── tokenizer.pkl
│
├── static/
│   ├── index.html
│   ├── script.js
│   └── style.css
│
├── main.py
├── requirements.txt
├── runtime.txt
├── final_clean.ipynb
├── .gitignore
└── README.md
```

- `main.py` contains the FastAPI application and prediction workflow.
- `Artifacts/BiGRU_Model.keras` stores the trained model.
- `Artifacts/tokenizer.pkl` stores the tokenizer used to prepare text for the model.
- `static/index.html` defines the web page.
- `static/style.css` controls the interface styling.
- `static/script.js` handles frontend interactions.
- `requirements.txt` lists the Python dependencies.
- `runtime.txt` specifies the Python runtime configuration, if configured for the deployment.
- `final_clean.ipynb` contains the notebook used for development or experimentation.

## Run the Project Locally

If you want to explore the code or run Moodline on your own computer, follow these steps.

### Prerequisites

Install:

- Python compatible with the project's dependencies
- Git
- A code editor, such as Visual Studio Code

### 1. Clone the repository

Replace `YOUR-USERNAME` with your GitHub username and use your actual repository URL.

```bash
git clone https://github.com/YOUR-USERNAME/Emotion-Prediction.git
cd Emotion-Prediction
```

### 2. Create a virtual environment

On Windows PowerShell:

```powershell
python -m venv .venv
```

Activate it:

```powershell
.\.venv\Scripts\Activate.ps1
```

### 3. Install dependencies

```powershell
python -m pip install --upgrade pip
pip install -r requirements.txt
```

If installation fails, check that your Python version and package versions are compatible with the versions specified in `requirements.txt`.

### 4. Start the application

The FastAPI instance in this project is started with Uvicorn. From the project directory, run:

```powershell
uvicorn main:app --reload
```

Open the application in your browser:

http://127.0.0.1:8000

FastAPI's interactive API documentation is generally available at:

http://127.0.0.1:8000/docs

Keep the terminal open while using the application. Press `Ctrl + C` to stop the local server.

## Limitations

Moodline is an experimental emotion classification application, and its predictions have some limitations.

- **Context matters:** A short sentence may not provide enough information to identify the intended emotion.
- **Mixed emotions:** A message can express several emotions at the same time, while the model may select only one primary category.
- **Sarcasm and figurative language:** The intended meaning may differ from the literal words in a sentence.
- **Training data:** The model may perform differently on text that differs from its training examples.
- **Confidence scores:** A high score does not necessarily mean that a prediction is correct or well calibrated.

The application predicts patterns in text. It does not know what a person is actually feeling, and its output should not be treated as a psychological assessment.

## What I Learned

Building Moodline gave me an opportunity to work with a deep learning model beyond the training stage and connect it to a complete web application.

The project helped me explore how text is converted into numerical input, how a trained model produces class predictions, and how those results can be presented through a frontend.

It also gave me practical experience working with saved model artifacts, a tokenizer, a FastAPI backend, and a deployed application.

## Future Improvements

Some improvements I would like to explore include:

- Evaluating the model on a separate test dataset and documenting its performance
- Improving handling of spelling variations and informal language
- Adding examples to help users understand the different emotion categories
- Improving error handling for empty or unusually long inputs
- Making the interface more accessible across devices
- Adding automated tests for preprocessing and prediction endpoints

## Disclaimer

Moodline is a machine learning project intended for educational and demonstration purposes. Its predictions are estimates generated by a trained model and may be incorrect. They should not be used to make important decisions about a person's mental health, emotional state, or well-being.

---

**Built with Python, TensorFlow, FastAPI, and a little curiosity about how we express emotions through text.**
