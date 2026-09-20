# 🛡️ AI Traffic Shield — Bot Detector

A machine learning-based web traffic analysis system designed to detect **automated/bot traffic** and distinguish it from **human/legitimate traffic** using behavioural characteristics of web requests.

This project combines **Cybersecurity, Web Traffic Analysis, and Machine Learning** to identify suspicious automated activity such as scrapers, scanners, headless browsers, and brute-force behaviour.

## 🎯 Project Objective

The objective of **AI Traffic Shield** is to analyse behavioural features from web traffic sessions and classify each session as:

* `0` → Human / Legitimate Traffic
* `1` → Automated / Bot Traffic

The project demonstrates how machine learning can be applied to cybersecurity telemetry and web traffic analysis.

## 🔍 Key Features

* 📊 Web traffic behavioural analysis
* 🤖 Machine learning-based bot detection
* 🔐 Cybersecurity-oriented feature analysis
* 📈 Exploratory Data Analysis (EDA)
* 🧠 Logistic Regression classification
* ⚖️ Train/test split with stratification
* 📏 Feature standardization using StandardScaler
* 📋 Confusion matrix and classification metrics
* 🧪 Manual traffic-session prediction
* 🖥️ Interactive Jupyter Notebook dashboard using `ipywidgets`
* 💾 Saved trained model and scaler

## 🧠 Machine Learning Workflow

```text
Web Traffic Dataset
        ↓
Data Inspection & Cleaning
        ↓
Exploratory Data Analysis
        ↓
Feature Selection
        ↓
Train/Test Split
        ↓
Feature Standardization
        ↓
Logistic Regression
        ↓
Model Evaluation
        ↓
Traffic Classification
        ↓
Interactive Dashboard
```

## 📂 Dataset

The dataset contains **30,000 web traffic sessions** with behavioural features describing how users or automated systems interact with a web application.

### Traffic Distribution

| Traffic Class      |    Samples |
| ------------------ | ---------: |
| Human / Legitimate |     12,500 |
| Automated / Bot    |     17,500 |
| **Total**          | **30,000** |

The dataset includes different traffic profiles such as:

* Human
* Returning Visitor
* API Client
* Scraper
* Polite Scraper
* Headless Browser
* Scanner
* Brute Force

## 📊 Features Used

The final model uses 14 behavioural features:

| Feature               | Description                                   |
| --------------------- | --------------------------------------------- |
| `request_count`       | Total number of requests in a session         |
| `distinct_paths`      | Number of unique paths requested              |
| `path_repeat_ratio`   | Ratio of repeated paths                       |
| `path_entropy`        | Diversity of requested paths                  |
| `static_asset_ratio`  | Proportion of requests for static assets      |
| `error_rate`          | Rate of erroneous requests                    |
| `not_found_rate`      | Rate of HTTP 404 requests                     |
| `auth_failure_rate`   | Rate of failed authentication attempts        |
| `auth_failure_count`  | Number of authentication failures             |
| `distinct_usernames`  | Number of different usernames attempted       |
| `requests_per_minute` | Request frequency                             |
| `interval_cv`         | Coefficient of variation of request intervals |
| `max_depth`           | Maximum URL/path depth                        |
| `distinct_depths`     | Number of distinct path depths                |

The `distinct_user_agents` feature was removed because it contained a constant value and therefore did not provide useful variation for the model.

## 🤖 Machine Learning Model

### Logistic Regression

The project uses **Logistic Regression** as the classification model.

Numerical features were standardized using:

```python
StandardScaler()
```

### Dataset Split

```text
Training Data : 24,000 samples
Testing Data  : 6,000 samples
Split         : 80% / 20%
Random State  : 42
Stratified    : Yes
```

## 📈 Model Performance

The model was evaluated on the **6,000-sample test dataset**.

| Metric    |      Result |
| --------- | ----------: |
| Accuracy  |  **99.87%** |
| Precision | **100.00%** |
| Recall    |  **99.77%** |
| F1-Score  |  **99.89%** |

### Confusion Matrix

```text
                 Predicted
                 Human   Bot

Actual Human      2500    0
Actual Bot           8  3492
```

The model correctly classified **5,992 out of 6,000 test samples**.

> **Note:** These results represent performance on this project's test dataset. They should not be interpreted as guaranteed real-world bot-detection accuracy.

## 🖥️ Interactive Dashboard

The project includes an interactive dashboard built directly inside the Jupyter Notebook using **ipywidgets**.

Users can enter traffic characteristics such as:

* Request count
* Request frequency
* Path behaviour
* Error rate
* Authentication failures
* Path entropy
* Session timing behaviour

The dashboard then predicts whether the traffic is:

```text
🟢 HUMAN / LEGITIMATE TRAFFIC
```

or:

```text
🔴 AUTOMATED / BOT TRAFFIC
```

## 🧪 Example Prediction

An example suspicious traffic session containing:

* High request frequency
* High error rate
* Multiple authentication failures
* Repeated paths
* Low interval variation

was classified by the model as:

```text
Automated / Bot Traffic
```

## 📁 Project Structure

```text
AI-Traffic-Shield-Bot-Detector/
│
├── AI_Traffic_Shield_Bot_Detector.ipynb
├── AI_Traffic_Shield_Bot_Detector.csv
├── bot_detection_model.pkl
├── bot_detection_scaler.pkl
└── README.md
```

### File Description

**`AI_Traffic_Shield_Bot_Detector.ipynb`**
Main Jupyter Notebook containing data analysis, preprocessing, model training, evaluation, prediction, and the interactive dashboard.

**`AI_Traffic_Shield_Bot_Detector.csv`**
Dataset used for training and evaluating the model.

**`bot_detection_model.pkl`**
Saved trained Logistic Regression model.

**`bot_detection_scaler.pkl`**
Saved StandardScaler used during model training.

**`README.md`**
Project documentation and overview.

## 🛠️ Technologies Used

### Programming & Data Science

* Python
* Pandas
* NumPy
* Scikit-learn
* Matplotlib
* Jupyter Notebook

### Machine Learning

* Logistic Regression
* StandardScaler
* Classification Metrics
* Confusion Matrix

### Interactive Interface

* IPyWidgets
* HTML
* CSS

### Cybersecurity Concepts

* Web Traffic Analysis
* Bot Detection
* Automated Activity Detection
* Authentication Failure Analysis
* Request Behaviour Analysis
* Security Analytics

## 🔐 Cybersecurity Relevance

This project demonstrates how machine learning can be applied to cybersecurity telemetry and web traffic analysis.

Behavioural indicators such as:

* High request rates
* Repeated path access
* HTTP errors
* Authentication failures
* Unusual session timing
* Scanner-like behaviour

can provide useful signals for identifying automated activity.

The project provides a foundation for further development in areas such as **SOC monitoring, security analytics, web application security, and automated threat detection**.

## ⚠️ Limitations

The current project has several limitations:

* The dataset is a prepared dataset rather than live production traffic.
* The model is evaluated using data from this project dataset.
* Real-world web traffic can contain more complex behaviours.
* Attackers may modify their behaviour to evade detection.
* Performance may change when the model is applied to different environments.
* The current implementation performs session-level classification rather than continuous real-time monitoring.

## 🚀 Future Scope

Possible future improvements include:

* Real-time web server log ingestion
* Continuous traffic monitoring
* Automated security alerts
* SIEM integration
* Model retraining using real-world traffic
* Additional behavioural features
* Detection of evolving bot behaviour
* API-based deployment
* Integration into a SOC monitoring workflow
* Explainable AI for security analysts

## 📌 Disclaimer

This project is developed for **educational, cybersecurity learning, and research purposes**.

The system demonstrates machine learning-based behavioural analysis and should not be considered a complete production-grade bot detection or security solution.


## 👩‍💻 Author

**Valentina**
BSc Information Technology Student | Cybersecurity & Machine Learning Enthusiast

### 🔐 Areas of Interest

* Cybersecurity
* Security Operations & Threat Detection
* Machine Learning
* Network Security
* AI & Security
* Data Analysis

### 🛠️ Technical Skills

* **Languages:** Python, Java, C, JavaScript, PHP, SQL
* **Database:** PostgreSQL, SQL
* **Cybersecurity:** Networking, Linux, Security Fundamentals
* **Machine Learning:** Pandas, NumPy, Scikit-learn, Matplotlib
* **Tools:** Jupyter Notebook, Git & GitHub, Canva,VScode

### 📌 Current Focus

Building practical projects that combine **Cybersecurity, Machine Learning, and AI**, while developing industry-ready technical skills through hands-on projects and internships.

### 🌐 Connect

🔗 LinkedIn:www.linkedin.com/in/valentina-john-66913b42b
💻 GitHub: https://github.com/johnvalentina1413-stack
