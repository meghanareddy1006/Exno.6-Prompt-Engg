# Date:14/5/25
# Register no.212222060142
Aim:
To develop a Python script compatible with multiple AI tools that automates API interaction, compares outputs, and generates actionable insights.

Objective:
Design a Python-based solution that:

Connects to multiple AI services via APIs
Sends standardized prompts or inputs
Collects and stores the responses
Evaluates the outputs based on quality, tone, performance, or accuracy
Produces reports or logs for analysis
This approach facilitates benchmarking of AI tools and helps identify the most suitable one for specific tasks.

Procedure / Algorithm:
Step 1: Define the Use Case
Select a task that can be evaluated across different AI platforms, such as:

Text summarization
Image generation
Sentiment analysis
Translation
Audio synthesis
Example: Compare the summarization abilities of ChatGPT (OpenAI) and Cohere.

Step 2: Configure API Access
Register for API access and store API keys securely using environment variables.

import os

OPENAI_API_KEY = os.getenv("OPENAI_API_KEY")
COHERE_API_KEY = os.getenv("COHERE_API_KEY")
Step 3: Define API Interaction Functions
Create functions to send requests and retrieve responses from each AI tool.

import openai
import cohere

def get_openai_summary(text):
    openai.api_key = OPENAI_API_KEY
    response = openai.ChatCompletion.create(
        model="gpt-4",
        messages=[{"role": "user", "content": f"Summarize this: {text}"}]
    )
    return response['choices'][0]['message']['content']

def get_cohere_summary(text):
    co = cohere.Client(COHERE_API_KEY)
    response = co.summarize(text=text)
    return response.summary
Step 4: Provide Input Data
Prepare a set of texts to be summarized by both tools.

test_inputs = [
    "Artificial intelligence (AI) is rapidly evolving and...",
    "Climate change is one of the most pressing issues..."
]
Step 5: Collect and Compare Outputs
Loop through inputs, retrieve outputs, and store results.

results = []

for text in test_inputs:
    openai_output = get_openai_summary(text)
    cohere_output = get_cohere_summary(text)
    
    results.append({
        "input": text,
        "openai_summary": openai_output,
        "cohere_summary": cohere_output
    })
Step 6: Analyze Outputs
Evaluate each summary using metrics such as word count and sentiment.

from textblob import TextBlob

def analyze_summary(summary):
    blob = TextBlob(summary)
    return {
        "word_count": len(summary.split()),
        "sentiment": blob.sentiment.polarity,
        "readability": blob.sentiment.subjectivity
    }

for result in results:
    result["openai_analysis"] = analyze_summary(result["openai_summary"])
    result["cohere_analysis"] = analyze_summary(result["cohere_summary"])
Step 7: Generate Summary Report
Export the comparative analysis to a file for further use.

import json

with open("summary_comparison.json", "w") as f:
    json.dump(results, f, indent=4)
Result:
The Python script was successfully executed to:

Connect with multiple AI tools using their APIs
Send uniform prompts to each service
Collect and compare responses using linguistic metrics
Generate structured output for evaluation and reporting
Conclusion:
This experiment effectively demonstrates how Python can integrate multiple AI services for comparative benchmarking. It supports:

Informed selection of the best-performing AI model
Automated, consistent evaluation pipelines
Scalable applications across tasks like content generation, sentiment analysis, and summarization
Such systems can be extended for complex use cases including multi-AI chatbots, research comparison platforms, and hybrid AI workflows.

Final Result:
The corresponding prompt-based Python automation was executed successfully.
