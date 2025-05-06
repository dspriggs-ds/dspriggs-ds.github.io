---
layout: default
title:  "Using OpenAI and Python to Power Fantasy Football Insights"
date:   2025-04-29 14:10:46 -0700
categories: Azure OpenAI Python
---

Fantasy Football has become a data-driven sport, and with the right tech stack, you can generate player-specific weekly predictions and insights like a pro. In this blog post, I’ll walk you through how I built a **Flask web app** that uses **OpenAI’s GPT via Azure**, the **nfl_data_py** package, and some smart Python logic to deliver fantasy football analysis on demand.

---

## 💡 Project Overview

The app allows users to:
- Select an NFL player and a specific week
- Query historical weekly stats for that player
- Send the data to an **OpenAI GPT model fine-tuned for fantasy football**
- Return and display **AI-generated predictions and insights**

All of this is wrapped in a simple Flask interface that lets any football fan get personalized analysis at the click of a button.

---

## 🧱 Technology Stack

- **Flask**: Lightweight web server with WTForms for user input
- **nfl_data_py**: Pulls current and historical NFL data
- **OpenAI (Azure)**: Delivers player analysis based on historical performance
- **Markdown**: Renders rich AI output safely in HTML

---

## 🔍 How It Works

### 1. User Interface (`app.py`)

The root route ("/") provides a form where users select a player and week number. On submission, Flask passes the input to the `get_analysis()` function which retrieves and analyzes weekly stats.

```python
@app.route("/", methods=['GET', 'POST'])
def home():
    form = fantballForm()
 
    if form.validate_on_submit():
        week = form.weeklist.data
        player_id = form.playerslist.data
        player_name = data.get_player_name(player_id)
        ret_value = markdown.markdown(data.get_analsysis(player_id, player_name, week))
        return render_template('display.html', analysis_text=ret_value)
    
    return render_template('index.html', form=form, title='Fantasy Football Analysis')
```

### 2. Data Preparation (`data.py`)

The `get_analsysis()` function fetches up to 5 years of weekly player data using `nfl_data_py`. It filters for the selected player, drops extraneous columns, and converts the data to JSON.

```python
weekly_data = nfl.import_weekly_data(year_season)
weekly_data = weekly_data[weekly_data['player_id'] == player_id]
content = weekly_data.to_json(orient="records")
```

### 3. GPT-Driven Prediction

We then format a prompt for the GPT model and send it along with the weekly stats via the Azure OpenAI client.

```python
prompt = f"Provide Fantasy Football Analysis for {player_name} and predicted score for Week {week}..."
response = client.chat.completions.create(
    model="fantfootball",
    messages=[
        {"role": "system", "content": "You are a Fantasy Football expert."},
        {"role": "user", "content": content + "\n\n" + prompt},
    ],
)
```

The AI returns an **expert-like analysis** of the player's past performance and likely outcome for the selected week — all in plain English.

---

## 📸 Example Output

Selecting a player like **Patrick Mahomes** for **Week 15** might return insights like:

> *“Patrick Mahomes has shown strong consistency in red zone completions across the last five seasons. Based on his passing yardage trends and KC’s matchup history, he is projected to earn 24.8 fantasy points in Week 15…”*

The model handles both qualitative and quantitative summaries, making it a fantastic tool for fans and analysts alike.

---

## 🔐 Securing Secrets

API keys and endpoints are stored in a `.env` file and loaded securely using `python-dotenv`:

```python
openai.api_key = os.getenv('openaikey')
openai.base_url = os.getenv('openaiendpoint')
```

This protects sensitive credentials while keeping them easily configurable for different environments.

---

## 🚀 Want to Build It Yourself?

Here’s what you’ll need to get started:
1. <a href="https://learn.microsoft.com/en-us/azure/cognitive-services/openai/">Azure OpenAI access</a>
2. <a href="https://pypi.org/project/nfl-data-py/">nfl_data_py</a> for player stats
3. Flask for the web interface
4. Basic HTML templates to render the form and results

---

## 🌟 Final Thoughts

This app blends real NFL data with the predictive power of GPT to deliver customized fantasy football insights in seconds. It's just one example of how **AI can empower sports fans** and bring advanced analytics to everyone.

If you’re a Fantasy Football enthusiast, this app could be your new best friend for weekly matchups and trade decisions!

## 🔗 Try It Yourself

You can check out the <a href="https://github.com/dspriggs-ds/fantfootballai">GitHub repository</a> to access the code, data links, and dashboard setup instructions. All you need is an Azure Databricks account to get started.
