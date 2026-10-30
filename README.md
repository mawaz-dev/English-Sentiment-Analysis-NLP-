# 💬 English Sentiment Analysis (NLP)

A beginner-friendly NLP project that classifies English text as **Positive** or **Negative**. It covers the full workflow: text cleaning, TF-IDF features, a Naive Bayes classifier, and a small Flask web app for real-time predictions.

![Python](https://img.shields.io/badge/Python-3.10-3776AB?logo=python&logoColor=white)
![Flask](https://img.shields.io/badge/Flask-3.1-000000?logo=flask)
![scikit-learn](https://img.shields.io/badge/scikit--learn-1.7-F7931E?logo=scikit-learn&logoColor=white)
![NLTK](https://img.shields.io/badge/NLTK-3.9-green)
![License](https://img.shields.io/badge/License-MIT-blue.svg)

---

## ✨ Features

- 🧹 **Text preprocessing** – Removes non-letters, lowercases, and filters NLTK English stopwords
- 🔢 **TF-IDF vectorization** – Converts text to numeric features
- 🤖 **Multinomial Naive Bayes** – Fast, classic text classifier
- 🌐 **Flask web app** – Type text in the browser and get an instant result
- 🔌 **JSON API** – `POST /predict` for use from other apps
- 📓 **Documented notebook** – Step-by-step walkthrough from data loading to evaluation

## 🖥️ Example

| Input | Output |
|---|---|
| "I love this product!" | Positive |
| "This is terrible and frustrating." | Negative |

## 🧰 Tech Stack

Python · Flask · scikit-learn · NLTK · pandas · joblib · HTML/CSS/JavaScript

## 📁 Project Structure

```
├── app.py                           # Flask app, preprocessing, /predict endpoint
├── templates/index.html             # Web UI
├── english_sentiment_analysis.ipynb # Full training and evaluation notebook
├── sentiment_data.csv               # Full dataset (~241k comments)
├── sample_comments.csv              # Balanced 100-row sample used for training
├── cleaned_sample_tweets.csv        # Cleaned version of the sample
├── naive_bayes_model.pkl            # Trained model
├── tfidf_vectorizer.pkl             # Fitted TF-IDF vectorizer
└── requirements.txt
```

## 📊 Dataset

The notebook uses the [Sentiment Analysis Dataset](https://www.kaggle.com/datasets/abdelmalekeladjelet/sentiment-analysis-dataset/data) from Kaggle: about 241,000 comments with three labels.

| Label | Meaning | Count |
|:---:|---|---:|
| 0 | Negative | 55,114 |
| 1 | Neutral | 82,972 |
| 2 | Positive | 103,059 |

For binary classification, only labels `0` (Negative) and `2` (Positive) are used.

## 🔄 How It Works

1. The user enters text in the web UI or sends a `POST` request to `/predict`.
2. The text is cleaned: non-letters removed, lowercased, stopwords dropped.
3. The saved TF-IDF vectorizer turns the text into a feature vector.
4. The Naive Bayes model predicts the label (`0` → Negative, `2` → Positive).
5. The result is returned as JSON and shown in the browser.

## ⚙️ Getting Started

### Prerequisites

- Python 3.10

### Installation

```bash
git clone https://github.com/<your-username>/English-Sentiment-Analysis-NLP.git
cd English-Sentiment-Analysis-NLP

python -m venv .venv
source .venv/bin/activate        # Windows: .venv\Scripts\activate
pip install -r requirements.txt
```

### Run the app

```bash
python app.py
```

Open [http://localhost:5000](http://localhost:5000). NLTK stopwords are downloaded automatically on first run.

### Re-train the model

Open `english_sentiment_analysis.ipynb` in Jupyter and run all cells. This regenerates `naive_bayes_model.pkl` and `tfidf_vectorizer.pkl`.

## 🔌 API

**`POST /predict`** (form data)

```bash
curl -X POST -d "user_input=I love this product" http://localhost:5000/predict
```

```json
{ "sentiment": "Positive" }
```

Errors return JSON with an `error` message and status `400` (empty input) or `500`.

## ⚠️ Model Performance & Limitations

The included model is a **learning demo**, not a production classifier:

- It was trained on a balanced sample of only **100 comments** (80 train / 20 test), not the full dataset.
- The TF-IDF vectorizer is limited to **10 features** (`max_features=10`), so it sees very few words.
- On the 20-comment test set it reached **50% accuracy**.
- It supports only two classes and treats anything that isn't label `2` as Negative. Neutral text is not handled.

**To improve it:** train on the full `sentiment_data.csv`, raise `max_features` to several thousand, add n-grams (`ngram_range=(1, 2)`), include the neutral class, and compare with Logistic Regression or a transformer model.

## 🗺️ Roadmap

- [ ] Train on the full dataset with proper evaluation
- [ ] Add a Neutral class
- [ ] Try Logistic Regression / SVM / transformer models
- [ ] Show prediction confidence in the UI
- [ ] Deploy online (Render / Hugging Face Spaces)

## 🤝 Contributing

Pull requests are welcome. For major changes, please open an issue first.

## 📄 License

This project is released under the MIT License.
