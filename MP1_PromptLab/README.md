# Project: Week 5_Graded Mini Project_HaimantiNag_MP1_PromptLab — Prompt Strategy Comparison

## 1. Project Overview

This project evaluates different prompt engineering strategies for extracting structured information from job description snippets using Large Language Models (LLMs).

The objective is to compare four prompting strategies based on extraction accuracy, parsing reliability, LLM judge scores, API cost, and response latency.

The four strategies implemented are:

1. **Zero-shot prompting:** Extracts information without providing examples.
2. **Few-shot prompting:** Provides sample input-output examples to guide the model.
3. **Structured / Role-based prompting:** Uses role instructions and structured output requirements.
4. **Chain-of-Thought (COT) prompting:** Encourages the model to reason through the extraction task before returning structured output.

The experiment uses an OpenAI-compatible API endpoint and Python asynchronous API calls to evaluate all strategies across the same dataset.

## 2. Project Objectives

- Implement four different prompt engineering strategies.
- Extract company name, job role, and required years of experience from job descriptions.
- Compare extracted information against a golden/reference dataset.
- Evaluate extraction quality using accuracy and an LLM judge.
- Measure parsing success, API cost, and response latency.
- Identify the most suitable prompting strategy based on experimental results.

## 3. Project Structure

```text
Week5_Graded_Mini_Project_HaimantiNag/
│
├── docs/
│   ├── ADR/
│   └── 002_prompting_strategy_capstone.md
│
├── MP1_PromptLab/
│   ├── data/
│   │
│   ├── mp1_prompt_lab/
│   │   ├── .env
│   │   ├── MP1_Assignment.ipynb
│   │   ├── mp1_comparison.md
│   │   └── mp1_writeup.md
│   │
│   ├── README.md
│   └── requirements.txt
│
└── .gitignore
```

*Note: Adjust the notebook filename or folder paths if your actual project structure differs.*

## 4. Requirements

The project requires:

- Python 3.10 or later
- Jupyter Notebook or JupyterLab
- An OpenAI-compatible API key
- Internet connectivity for API requests

### Python Dependencies

The required Python packages are listed in `requirements.txt`.

Install them using:

```bash
pip install -r requirements.txt
```

The main dependencies include:

| Package       | Purpose                               |
| ------------- | ------------------------------------- |
| openai        | LLM API integration using AsyncOpenAI |
| python-dotenv | Loading environment variables         |
| pandas        | Data processing and comparison tables |
| ipykernel     | Jupyter notebook kernel               |
| jupyter       | Notebook execution environment        |

## 5. Environment Configuration

Create a `.env` file in the project root directory.

Add the following configuration:

```text
OPENAI_API_KEY=your_actual_api_key
OPENAI_BASE_URL=https://openai.vocareum.com/v1
MODEL=gpt-4o-mini
JUDGE_MODEL=gpt-4o
TEMPERATURE=0.0
```

Replace `your_actual_api_key` with your assigned API key.

The configuration specifies:

- `OPENAI_API_KEY`: API authentication key.
- `OPENAI_BASE_URL`: API endpoint.
- `MODEL`: Model used for extraction.
- `JUDGE_MODEL`: Model used to evaluate extraction quality.
- `TEMPERATURE`: Controls response randomness.

**Security:** Never commit your `.env` file or expose your API key in the notebook or GitHub repository.

## 6. How to Run the Project

### Step 1: Clone or open the project

Open the project directory in VS Code, JupyterLab, or your preferred development environment.

### Step 2: Install dependencies

Run:

```bash
pip install -r requirements.txt
```

### Step 3: Configure environment variables

Create and configure the `.env` file as described in Section 5.

### Step 4: Open the Jupyter Notebook

Open the notebook:

```text
MP1_PromptLab/notebooks/MP1_PromptLab.ipynb
```

### Step 5: Execute the notebook cells

Run the notebook cells sequentially.

The notebook is organized into the following stages:

| Step   | Description                                                       |
| ------ | ----------------------------------------------------------------- |
| Step 1 | Setup environment, initialize API client, and load datasets       |
| Step 2 | Define the four prompting strategies                              |
| Step 3 | Execute asynchronous LLM API calls and collect extraction results |
| Step 4 | Score extracted results against the golden set                    |
| Step 5 | Aggregate metrics and generate the comparison table               |
| Step 6 | Write the experiment reflection and conclusions                   |

### Step 6: Review the results

After execution, review the final comparison table generated in Step 5.

It summarizes the performance of all four prompting strategies.

## 7. Evaluation Methodology

Each strategy is evaluated using the same job description snippets and golden/reference answers.

Three fields are evaluated:

- `company`
- `role`
- `years_experience_required`

The experiment uses the following metrics:

### 7.1 Mean Accuracy (0–3)

Measures how many of the three extracted fields match the golden set.

- 0 = No fields match.
- 1 = One field matches.
- 2 = Two fields match.
- 3 = All three fields match.

### 7.2 Parse Success (%)

Measures the percentage of LLM responses successfully parsed into structured JSON.

A higher percentage indicates better output formatting and parsing reliability.

### 7.3 Mean Judge Score (1–25)

An LLM judge evaluates the quality of extracted information on a scale of 1–4.

The score is converted to a 1–25 scale using:

```text
Converted Score = 1 + (Original Score - 1) * 8
```

### 7.4 Total Cost (USD)

Estimates the total API cost for each prompting strategy using the configured model token rates.

Actual provider billing may differ.

### 7.5 Median Latency (Seconds)

Measures the median time taken to complete an API request.

Lower latency indicates faster response time.

## 8. Experimental Results

The following table summarizes the results obtained from the experiment. It compares the four prompting strategies based on mean accuracy, parse success rate, LLM judge score, total API cost, and median latency.

| Strategy                | Mean Accuracy (0–3) | Parse Success (%) | Mean Judge Score (1–25) | Total Cost (USD) | Median Latency (seconds) |
| :---------------------- | -------------------: | ----------------: | -----------------------: | ---------------: | -----------------------: |
| COT                     |                  2.9 |             100.0 |                     25.0 |         0.000520 |                    8.903 |
| Few shot                |                  3.0 |             100.0 |                     25.0 |         0.000602 |                    4.423 |
| Structured / Role based |                  2.9 |             100.0 |                     25.0 |         0.000565 |                    6.486 |
| Zero shot               |                  2.9 |             100.0 |                     25.0 |         0.000464 |                    2.358 |

Few-shot prompting offers a good starting point when extraction accuracy is the priority.
while Zero-shot prompting which Achieved a mean accuracy of 2.9 and had the lowest estimated cost of $0.000466,Had the fastest median latency of 2.001 seconds, is a good choice when speed and cost efficiency are important.

Structured / Role-based prompting achieved a mean accuracy of 2.9 , maintained 100% parse success, provides explicit instructions and structured output requirements.

COT prompting achieved a mean accuracy of 2.9, had the highest median latency of 8.920 seconds, may be less efficient for relatively simple extraction tasks.

### 8.1 Key Findings and Interpretation of Results

- **Best accuracy:** Few-shot prompting (3.0 out of 3).
- **Best parse success:** All four strategies (100%).
- **Best judge score:** All four strategies (25 out of 25).
- **Lowest cost:** Zero-shot prompting ($0.000464).
- **Fastest response:** Zero-shot prompting (2.358 seconds).

Overall, Few-shot prompting achieved the highest extraction accuracy, while Zero-shot prompting offered the best cost and latency performance.

### 8.2 Overall Conclusion

Few-shot prompting performed best in terms of extraction accuracy, while Zero-shot prompting performed best in terms of cost and latency.
All four strategies achieved 100% parse success and a mean judge score of 25 out of 25.
The results demonstrate that the best prompting strategy depends on the application requirements and the trade-off between accuracy, speed, and cost.

## 9. Troubleshooting

Problem
Possible Solution
API authentication error (401)
Verify the API key and API endpoint in .env
Missing environment variables
Check the .env file location and reload it
ModuleNotFoundError
Run pip install -r requirements.txt
FileNotFoundError
Verify the dataset paths and notebook working directory
JSON parsing failure
Inspect the raw LLM response and prompt instructions
API rate-limit error
Reduce concurrent requests or add retry logic
Judge evaluation failure
Verify the judge model and API configuration

## 10. Future Improvements

Potential improvements include: Testing additional LLM models, Evaluating a larger and more diverse dataset, Refining prompts to handle ambiguous job descriptions, Combining few-shot examples with structured output instructions, Improving the LLM judge evaluation rubric, Comparing additional metrics such as precision, recall, and F1-score, Optimizing API costs and response latency.

## 11. Technologies Used

Python
Jupyter Notebook
OpenAI-compatible API
GPT-4o-mini
GPT-4o
AsyncOpenAI
Pandas
Python-dotenv

## 12. Author and Project Information

Project: Week 5_Graded Mini Project_HaimantiNag
Assignment: Prompt Strategy Comparison
Objective: Evaluate and compare prompting strategies for structured information extraction using Large Language Models.
