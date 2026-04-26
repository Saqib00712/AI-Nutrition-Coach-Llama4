# AI Nutrition Coach
> A multimodal AI web application that analyzes food images and provides detailed nutritional assessments — including calorie counts, nutrient breakdowns, and health evaluations — powered by Meta Llama 4 Maverick (17B) via IBM WatsonX and a clean Flask web interface.

---

## What This Project Does

Upload a photo of any meal and ask a nutrition question. The AI analyzes the image and returns a complete nutritional report in seconds.

```
Food Image + Question
        ↓
[Llama 4 Maverick 17B] — multimodal vision + language model
        ↓
Nutritional Assessment:
  - Food item identification
  - Portion size + calorie estimation
  - Total calorie count
  - Protein / Carbs / Fats / Vitamins breakdown
  - Health evaluation paragraph
  - Medical disclaimer
        ↓
Flask Web UI — clean results page with downloadable output
```

---

## Demo

**Input:** Photo of a salmon and asparagus plate

**Question:** *"How many calories are in this food?"*

**Output:**
```
1. Identification:
   - Salmon fillet
   - Asparagus spears
   - Cherry tomatoes

2. Portion Size & Calorie Estimation:
   - Salmon: 6 ounces, 210 calories
   - Asparagus: 3 spears, 25 calories
   - Cherry Tomatoes: 5 pieces, 15 calories

3. Total Calories: 250 calories

4. Nutrient Breakdown:
   - Protein: Salmon (35g), Asparagus (3g) = 38g total
   - Carbohydrates: Asparagus (5g), Tomatoes (3g) = 8g total
   - Fats: Salmon (12g) = 12g total

5. Health Evaluation:
   This is a highly nutritious, well-balanced meal rich in
   omega-3 fatty acids, lean protein, and essential vitamins...

6. Disclaimer: Nutritional values are approximate...
```

---

## Architecture

```
User uploads image + types question (Flask form)
        ↓
input_image_setup() — reads file, encodes to base64
        ↓
generate_model_response()
  → builds multimodal message (text + image_url)
  → sends to Llama 4 Maverick 17B via IBM WatsonX chat API
  → receives structured nutritional assessment
        ↓
format_response()
  → converts **bold** → <strong> HTML
  → converts * bullets → <ul><li> HTML
  → ensures proper line breaks
        ↓
Flask renders index.html with formatted response
```

---

## Tech Stack

![Python](https://img.shields.io/badge/Python-3.10+-blue?style=flat-square)
![Llama 4](https://img.shields.io/badge/Meta-Llama%204%20Maverick%2017B-purple?style=flat-square)
![IBM WatsonX](https://img.shields.io/badge/IBM-WatsonX-blue?style=flat-square)
![Flask](https://img.shields.io/badge/Flask-Web%20Framework-black?style=flat-square)
![PIL](https://img.shields.io/badge/Pillow-Image%20Processing-green?style=flat-square)

- **Meta Llama 4 Maverick (17B)** — multimodal vision + language model via IBM WatsonX
- **IBM WatsonX ModelInference** — chat API with `TextChatParameters`
- **Flask** — lightweight Python web framework for routing and templating
- **Jinja2** — HTML templating with `{{ response|safe }}` for formatted output
- **Pillow (PIL)** — image handling
- **Base64 encoding** — converting images to data URLs for multimodal API input
- **Regex formatting** — converting markdown-style response to clean HTML

---

## Project Structure

```
AI-Nutrition-Coach/
│
├── app.py                    # Flask backend — routes, model inference, formatting
├── templates/
│   └── index.html            # Main UI — upload form + results display
├── static/
│   └── style.css             # Custom CSS — responsive, clean design
├── requirements.txt          # All dependencies
├── .env.example              # API key template (for local use)
└── README.md
```

---

## Getting Started

### 1. Clone the repo
```bash
git clone https://github.com/Saqib00712/AI-Nutrition-Coach.git
cd AI-Nutrition-Coach
```

### 2. Install dependencies
```bash
pip install -r requirements.txt
```

### 3. Set up API key (only needed outside IBM Skills Network)
```bash
cp .env.example .env
```
Edit `.env`:
```
WATSONX_API_KEY=your_ibm_watsonx_api_key_here
WATSONX_PROJECT_ID=your_project_id_here
```

> If running inside IBM Skills Network, no API key is needed — the environment is pre-configured with `project_id="skills-network"`.

### 4. Run the app
```bash
python app.py
```

### 5. Open your browser
```
http://127.0.0.1:5000
```
Upload a food photo, type your question, and click **"Tell me the total calories"**.

---

## Key Concepts Covered

- **Multimodal AI** — sending both image and text in a single API call using `image_url` message format
- **Base64 image encoding** — converting uploaded files to base64 strings for API transmission
- **IBM WatsonX ModelInference** — using `model.chat()` with structured message objects
- **Llama 4 Maverick 17B** — state-of-the-art vision-language model for food recognition
- **Flask routing** — handling GET and POST requests with `@app.route`
- **Jinja2 templating** — rendering dynamic content with `{{ response|safe }}`
- **Regex-based HTML formatting** — converting `**bold**` and `* bullets` to proper HTML
- **Flash messages** — user-friendly error handling for missing files
- **JavaScript image preview** — displaying uploaded image before submission using `FileReader`
- **Structured prompting** — enforcing consistent output format via detailed system prompt

---

## Nutritional Assessment Format

The system prompt enforces a strict 6-section output structure:

| Section | Content |
|---------|---------|
| **Identification** | Lists each food item found in the image |
| **Portion Size & Calories** | Estimated portion and calories per item |
| **Total Calories** | Sum of all item calories |
| **Nutrient Breakdown** | Protein, Carbs, Fats, Vitamins, Minerals |
| **Health Evaluation** | One-paragraph health assessment |
| **Disclaimer** | Standard nutritional disclaimer |

---

## Customization

The `assistant_prompt` in `app.py` can be changed to support different use cases:

```python
# Current: Nutritionist mode
assistant_prompt = "You are an expert nutritionist..."

# Custom examples:
# "You are a fitness coach analyzing pre-workout meals..."
# "You are a chef identifying ingredients in this dish..."
# "You are a dietitian analyzing this meal for diabetic patients..."
```

---

## Related Certifications

Built as part of the IBM **Build Multimodal Generative AI Applications** and **Generative AI Engineering with Transformers & LLMs** Specializations on Coursera.

[![IBM Badge](https://img.shields.io/badge/IBM-Multimodal%20AI%20Applications-blue?style=flat-square)](https://www.credly.com/users/muhammad-saqib.361f9b8c)
[![IBM Badge](https://img.shields.io/badge/IBM-Generative%20AI%20Engineering-blue?style=flat-square)](https://www.credly.com/users/muhammad-saqib.361f9b8c)

---

## Author

**Muhammad Saqib**
- GitHub: [@Saqib00712](https://github.com/Saqib00712)
- LinkedIn: [muhammad-saqib](https://www.linkedin.com/in/muhammad-saqib-68b9b3374/)
- Email: saqibkhosa649@gmail.com
- Credly: [15x IBM Certified](https://www.credly.com/users/muhammad-saqib.361f9b8c)
