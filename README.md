# ⚡ GENAI‑POST‑GENERATOR

Automatically analyzes past LinkedIn posts by an influencer and generates new posts that match their style for a given topic, length, and language.

---

## 🧾 Demo


## ✨ Features

* Automatic extraction of past influencer post topics, languages, and lengths.
* Supports English and Hinglish post generation.
* Few-shot learning: uses influencer’s past posts as stylistic examples.
* Streamlined flow: research topic → select options → generate new LinkedIn-style post.

---

## 🧠 How It Works

1. **Preprocessing**:

   * `preprocess.py` reads `data/raw_posts.json`, extracts metadata (line count, language, up to 2 tags) using `llm_helper.py` and LangChain→JSON parser.
   * Tags are unified to consistent labels.([GitHub][1], [GitHub][2])

2. **Post Generation**:

   * `post_generator.py` composes a prompt with topic, desired length (“Short”, “Medium”, “Long” mapped to line ranges), and language.
   * Few-shot examples from similar posts are added to guide the LLM.
   * `llm_helper.py` invokes the LLM to generate the new post.([GitHub][3], [GitHub][2])

3. **Main Interface**:

   * `main.py` ties preprocessing and generation into a Streamlit app (or console flow), allowing users to interactively select inputs and view generated output.

---

## 🧱 Tech Stack

* **Python 3.x**
* **LangChain Core/PromptTemplate** for prompt building and output parsing([GitHub][1])
* **LLM/API backend**—e.g. Groq Cloud or similar
* **Streamlit** (if GUI interface via `main.py`)
* **JSON files** for inspiration/few-shot data in `data/`

---

## 📁 Project Structure

```
├── data/
│   ├── raw_posts.json
│   └── processed_posts.json
├── few_shot.py
├── llm_helper.py
├── main.py
├── post_generator.py
├── preprocess.py
└── requirements.txt
```

* `data/`: source and enriched post data
* `few_shot.py`: filters example posts based on tags, length, language([GitHub][3], [GitHub][4])
* `llm_helper.py`: wraps LLM invocation logic
* `preprocess.py`: metadata extraction and tag unification for posts([GitHub][1])
* `post_generator.py`: prompt composition and response generation
* `main.py`: application entry, e.g. via Streamlit
* `requirements.txt`: project dependencies

---

## ⚙️ Requirements & Setup

1. **Clone** the repository
2. **Install dependencies**:

   ```bash
   pip install -r requirements.txt
   ```
3. **Configure API key** (e.g. Groq Cloud):

   * Add `.env` with `GROQ_API_KEY=your_api_key`
4. **Run**:

   ```bash
   streamlit run main.py
   ```

   or, for CLI mode:

   ```bash
   python main.py
   ```

---

## 🔧 Future Improvements

* Add more supported languages beyond English/Hinglish
* Enable multiple influencer profiles and style mixing
* Accept user-provided sample posts to fine-tune style
* Add UI controls for tone, hashtags, emojis, personalization
* Deploy as a web service with user authentication
* Evaluate generated content quality with human feedback loop
