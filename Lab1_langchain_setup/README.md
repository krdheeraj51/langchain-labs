### ✅ Lab Objectives:
By the end of this lab, you will:
1. Set up a Python environment for LangChain.
2. Use Hugging Face’s free models to avoid API costs.
3. Create a reusable prompt template.
4. Connect everything with a LangChain `LLMChain`.
5. Run your app and generate a fun fact.

---

### 🛠️ Step 1: Environment Setup

#### 🔹 Install Python (if not already installed)
Make sure Python 3.8+ is installed. You can check using:

```bash
python --version
```

#### 🔹 Create and activate a virtual environment
```bash
python -m venv langchain-lab
source langchain-lab/bin/activate  # or use .\langchain-lab\Scripts\activate on Windows
```

#### 🔹 Install LangChain and dependencies
```python
pip install langchain huggingface_hub python-dotenv
```

---

### 🗝️ Step 2: Get a Hugging Face API Token

1. Go to: [https://huggingface.co/settings/tokens](https://huggingface.co/settings/tokens)
2. Create a **Read** access token (free account works).
3. Create a `.env` file in your project directory:
```python
HUGGINGFACEHUB_API_TOKEN=your_token_here
```

---

### 📁 Step 3: Set Up Project Structure

Create the following files:

```
langchain-lab/
├── .env
├── app.py
└── requirements.txt
```

---

### ✏️ Step 4: Write Your LangChain App (app.py)

```python
import os
from dotenv import load_dotenv
from langchain.llms import HuggingFaceHub
from langchain.prompts import PromptTemplate
from langchain.chains import LLMChain

# Load the token from .env
load_dotenv()

# Initialize LLM using Hugging Face
llm = HuggingFaceHub(
    repo_id="google/flan-t5-small",
    model_kwargs={"temperature": 0.7, "max_length": 100}
)

# Create a reusable prompt
prompt = PromptTemplate(
    input_variables=["topic"],
    template="Tell me a fun and surprising fact about {topic}."
)

# Build the chain
chain = LLMChain(llm=llm, prompt=prompt)

# Run the app
topic = input("Enter a topic: ")
response = chain.run(topic)
print(f"\n🤖 Fun Fact: {response}")
```

---

### 🧪 Step 5: Run the Lab

In the terminal:

```python
python app.py
```

Try entering different topics like:
- space
- sharks
- chocolate
- history
