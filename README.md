# 📊 ReviewLens: Sentiment Analysis of Product Reviews

ReviewLens is an NLP web application that reads a product review and classifies it as **Positive**, **Neutral** or **Negative**. It combines a trained Machine Learning model with a rule-based VADER lexicon, and is deployed on Vercel as a serverless Flask API with a lightweight HTML/JS frontend.

🔗 **Live Demo:** [your-app.vercel.app](https://your-app.vercel.app)

---

## ✨ Features

- Classifies reviews into Positive, Neutral or Negative
- Hybrid approach: Logistic Regression (TF-IDF) + VADER lexicon
- SMOTE to handle class imbalance
- Custom text preprocessing (tokenization, stopword removal, stemming)
- REST API endpoint: `/api/predict`
- Responsive web UI
- Vercel-ready deployment

---

## 🧠 How It Works

1. The user types a review in the web UI.
2. The frontend sends it to `/api/predict`.
3. The text is cleaned: tokenization, stopword removal, stemming.
4. It is converted to numbers using TF-IDF.
5. The ML model predicts a sentiment, and VADER gives a lexicon-based score.
6. Both results are combined using confidence and vocabulary coverage.
7. The final label is returned and shown on the page.

```
Review → Preprocessing → TF-IDF → Logistic Regression ┐
                                                       ├→ Final Sentiment
                              VADER Lexicon Score ─────┘
```

---

## 🛠️ Tech Stack

| Layer | Technology |
|---|---|
| Language | Python |
| ML | Scikit-learn, Pandas, NLTK, imbalanced-learn (SMOTE) |
| Backend | Flask (REST API) |
| Frontend | HTML, CSS, Vanilla JavaScript |
| Model Storage | Joblib |
| Deployment | Vercel |

---

## 📁 Project Structure

```
ReviewLens/
├── api/
│   └── index.py          # Flask API (serverless entry point)
├── nltk_data/            # VADER lexicon (bundled for serverless)
├── index.html            # Frontend
├── preprocessing.py      # Text cleaning functions
├── train_model.py        # Model training script
├── model_handler.py      # Combines ML + VADER prediction
├── model.joblib          # Trained model
├── tfidf.joblib          # Trained TF-IDF vectorizer
├── reviews.csv           # Training dataset
├── requirements.txt
└── vercel.json           # Vercel routing config
```

---

## 🔌 API Usage

**Endpoint:** `POST /api/predict`

**Request**
```json
{ "text": "Amazing quality, totally worth it!" }
```

**Response**
```json
{ "sentiment": "Positive" }
```

---

## 📈 Model Performance

| Metric | Score |
|---|---|
| Accuracy | XX% |
| Dataset size | N reviews |
| Classes | Positive, Neutral, Negative |

> Run `python train_model.py` to see the full classification report.

---

## 🚀 Run Locally

```bash
# 1. Clone the repository
git clone https://github.com/your-username/ReviewLens.git
cd ReviewLens

# 2. Install dependencies
pip install -r requirements.txt

# 3. (Optional) Retrain the model
python train_model.py

# 4. Start the API
python api/index.py
```

Open `index.html` in your browser. For local testing, change the fetch URL in `index.html` to `http://localhost:5000/api/predict` and change it back to `/api/predict` before pushing.

---

## ☁️ Deploy on Vercel

1. Push the repository to GitHub.
2. Open the Vercel dashboard and click **Add New Project**.
3. Import your GitHub repository.
4. Keep the default build settings. `vercel.json` handles the routing:
   - `/` → `index.html`
   - `/api/*` → `api/index.py`
5. Click **Deploy**.

> The NLTK VADER data is stored inside the repo (`nltk_data/`) because serverless functions cannot download it at startup.

---

## 🔮 Future Improvements

- Hindi / Hinglish review support
- Confidence score and keyword highlights in the UI
- Batch review analysis via CSV upload
- Transformer-based model (DistilBERT) comparison

---

## 📄 License

This project is for educational purposes. Feel free to modify and use it.

---

## 👤 Author

**Sufiyan**
B.Tech CSE, Jamia Millia Islamia
[GitHub](https://github.com/sufiyann01)
