# Text to SQL in Farsi using LLM

 This repository, based on the article [Text-to-SQL Domain Adaptation via Human-LLM Collaborative Data Annotation](https://dl.acm.org/doi/10.1145/3708359.3712083), transforms Persian questions into SQL queries for a [Persian books dataset](https://www.kaggle.com/datasets/saeedtqp/persian-books-dataset). It leverages a language model and probabilistic grammar to generate queries, refining them with AST-based techniques. The system interactively processes user inputs, targeting a database with book details like price and categories. It aims to bridge natural language and structured queries effectively. The approach emphasizes human-LLM collaboration for domain-specific adaptation.
> [!NOTE]
> Code.ipynb is running on my Google Colab account using CPU.

## Dataset
The dataset used is sourced from [Kaggle: Persian Books Dataset](https://www.kaggle.com/datasets/saeedtqp/persian-books-datasettaset). It contains information about Persian books with the following schema:
- **Table**: `books`
- **Columns**:
  - `book_id` (integer): Book identifier
  - `title` (text): Book title
  - `description` (text): Book description
  - `price` (integer): Digital price (Toman)
  - `number_of_page` (integer): Number of pages
  - `PhysicalPrice` (integer): Physical price (Toman)
  - `publishDate` (text, YYYY/MM/DD): Publication date
  - `rating` (float): Rating
  - `publisher` (text): Publisher
  - `coveruri` (text): Cover image URL
  - `number_of_q` (integer): Number of questions
  - `categories` (text): Categories
  - `number_of_cm` (integer): Number of comments
  - `author_name` (text): Author name
  - `translator_name` (text): Translator name
  - `lang` (text): Language
  
```python
df.sample(n=1)
```
Output:
| book_id | title                                | description                                              | price | number_of_page | PhysicalPrice | publishDate | rating | publisher          | coveruri                                       | number_of_q | categories | number_of_cm | author_name    | translator_name | lang |
|---------|--------------------------------------|----------------------------------------------------------|-------|----------------|---------------|-------------|--------|-------------------|------------------------------------------------|-------------|------------|--------------|----------------|-----------------|------|
| 15266   | به خانه آمدم، هیچ کلمه‌ای در انتظارم نبود | «به خانه آمدم، هیچ کلمه‌ای در انتظارم نبود» سو...       | 4500  | 96             | 0             | 1397/10/17  | NaN    | انتشارات سوره مهر | https://img.taaghchecdn.com/frontCover/44590.jpg | 0           | شعر معاصر  | 0            | محمدرضا طبسی   | NaN             | Fa   |
## Features
- **Natural Language Processing**: Converts Persian questions into SQL queries.
- **PCFG**: Generates fallback SQL queries probabilistically when the LLM fails.
- **AST Refinement**: Ensures query correctness by comparing against reference SQL queries.
- **LLM Integration**: Uses the DeepSeek Chat model via OpenRouter API for query generation.
- **Interactive CLI**: Allows users to input questions and receive SQL queries in real-time.

## Requirements
- Python 3.x
- Libraries: `pandas`, `requests`, `sqlparse`, `difflib`, `sqlglot`
- Google Colab with Drive integration (optional)
- OpenRouter API key
  
## Usage
- Run the script and enter a question in Persian (e.g., "کتاب‌هایی که قیمتشون بیشتر از 8000 هستش").
- The system will output a corresponding SQL query (e.g., `SELECT * FROM books WHERE price > 8000;`).
- Type "بوس" to exit.
