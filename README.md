# 👨‍🍳 Chef-AI Agent

![Python](https://img.shields.io/badge/Python-3.10%2B-blue?style=for-the-badge&logo=python&logoColor=white)
![LangChain](https://img.shields.io/badge/LangChain-🦜️🔗-green?style=for-the-badge)
![Google Gemini](https://img.shields.io/badge/Google%20Gemini-8E75B2?style=for-the-badge&logo=google&logoColor=white)
![FAISS](https://img.shields.io/badge/FAISS-Vector%20Store-orange?style=for-the-badge)
![License](https://img.shields.io/badge/License-MIT-yellow?style=for-the-badge)

A context-aware **Culinary AI Agent** designed to act as a personalized sous-chef. This intelligent system leverages the **LangChain** framework and **Google's Gemini models** to orchestrate a suite of tools. The features include retrieving recipes from public APIs, accessing private cultural cookbooks via RAG, and performing real-time nutritional analysis while strictly adhering to user dietary preferences.

---

## 🏗️ Agent Framework & Architecture

The core of this project is built on **LangChain's Conversational ReAct Agent**. The agent utilizes a Thought-Action-Observation loop to dynamically select the right tool for the job.

### **Libraries & Frameworks**
* **[LangChain](https://www.langchain.com/):** The primary orchestration framework used to manage agent tools, memory (chat history), and the ReAct execution loop (`AgentType.CONVERSATIONAL_REACT_DESCRIPTION`).
* **[LangChain Google GenAI](https://pypi.org/project/langchain-google-genai/):** Handles the connection to Google's Gemini-1.5-Pro / Gemini-2.5-Flash models for reasoning and natural language generation.
* **[FAISS (Facebook AI Similarity Search)](https://github.com/facebookresearch/faiss):** Serves as the vector database for storing private recipes (PDFs) and user dietary preferences.
* **[PyPDF2](https://pypi.org/project/PyPDF2/):** Used for extracting raw text from private recipe documents for RAG (Retrieval Augmented Generation).

---

## 🔌 APIs Integrated

This agent acts as a central hub connecting multiple external data sources:

| API Name | Usage |
| :--- | :--- |
| **[Google Gemini API](https://ai.google.dev/)** | **The "Brain":** Used for reasoning, ingredient extraction, and final response generation. |
| **[TheMealDB API](https://www.themealdb.com/api.php)** | **Public Recipe Search:** Used to fetch general, international recipes (e.g., "Chicken Soup"). |
| **[API-Ninjas Nutrition](https://api-ninjas.com/api/nutrition)** | **Nutritional Analysis:** Used to calculate calories, fats, proteins, and carbs for specific ingredients or full recipes. |
| **Private Vector Store** | **RAG:** Acts as a custom API for retrieving specialized private recipes (e.g., "Onam Payasam") not found in public databases. |

---

## ✨ Key Features

* **🧠 Intelligent Tool Routing:** The agent decides whether to search the web, query the private database, or perform calculation analysis based on user intent.
* **🛡️ Dietary Preference Memory:** Persistently stores user constraints (e.g., *"I am allergic to raisins"*) in a vector store and automatically checks every recommendation against these constraints.
* **📚 Retrieval Augmented Generation (RAG):** Capabilities to read, chunk, and retrieve context from local PDF files (specifically tailored for authentic cultural recipes).
* **🥗 Automated Nutrition Auditing:** Extracts ingredients from unstructured text using LLMs and queries the Nutrition API to provide a health breakdown.
* **🔄 Self-Correction:** The agent logic includes a priority system—it attempts to find a recipe first, analyze it second, and modify it only if necessary.

---

## 🚀 Getting Started

### Prerequisites
* Python 3.10 or higher
* Jupyter Notebook or Google Colab environment

### Installation

1.  **Clone this repository**

2.  **Install the required Python packages**
    ```bash
    pip install langchain langchain-google-genai langchain-community faiss-cpu pypdf2 requests google-generativeai
    ```

3.  **Configure Environment Variables**
    Create a `.env` file or set these secrets in your Colab environment:
    ```python
    GOOGLE_API_KEY=your_google_gemini_key
    API_NINJAS_KEY=your_api_ninjas_key
    ```

4.  **Add Private Data**
    * Upload your `onam-recipes.pdf` (or any cookbook PDF) to the root directory to enable the RAG functionality.

### Usage

Run the Jupyter Notebook `Chef-AI_Agent.ipynb`. The agent will initialize and prompt you for input.

Launch the agent loop:

    main()

### Example Interaction

User:  
"Find me a recipe for Onam Payasam, but I'm allergic to raisins."

Agent behavior:  
- Checks preferences  
- Searches Private Vector Store  
- Modifies recipe to remove raisins  
- Outputs a safe recipe  

---

### 📂 Project Structure

    ├── Chef-AI_Agent.ipynb      # Main application notebook
    ├── onam-recipes.pdf         # Private knowledge base (PDF)
    ├── README.md                # Documentation
    └── requirements.txt         # Dependencies

---

### 🤝 Contributing

Contributions are welcome. Please fork the repository and create a pull request for any new features, such as adding LangGraph support or integrating new APIs.

---

### 📄 License

Distributed under the MIT License. See the LICENSE file for more information.
