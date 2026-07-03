# Homework: AI Orchestration with Kestra
ATTENTION: At the end of the submission form, you will be required to include a link to your GitHub repository or other public code-hosting site. This repository should contain your code for solving the homework. If your solution includes code that is not in file format, please include these directly in the README file of your repository.

`It's possible your answers won't match exactly. If so, select the closest one`

## Prerequisites
Before starting this homework, ensure you have:

1. Completed the Module 3 lessons — the questions reference flows and concepts covered there
2. Kestra running locally with API keys configured (see the Setup lesson) -- this includes the Gemini API key, which is also required for the AI Copilot
3. Imported all flows from the 03-orchestration/flows/ directory (covered in the Setup lesson)

## Question 1: Context Engineering
Try the following experiment:

1. Open ChatGPT in a private browser window: https://chatgpt.com
2. Enter this prompt: "Create a Kestra flow that loads NYC taxi data from CSV to BigQuery"
3. Then, use Kestra's AI Copilot with the same prompt

After trying the same prompt in ChatGPT vs Kestra's AI Copilot, what is the primary reason AI Copilot generates better Kestra flows?

1. AI Copilot uses a more powerful model
2. AI Copilot has access to current Kestra plugin documentation <-- answer
3. AI Copilot uses more tokens
4. AI Copilot has internet access

## Question 2: RAG vs No RAG
Run both 1_chat_without_rag.yaml and 2_chat_with_rag.yaml in the Kestra UI. Read the execution logs for each.

The non-RAG response about Kestra 1.1 features is best described as:

1. Accurate and specific, matching the actual release notes
2. Vague, generic, or fabricated — the model guesses from training data <-- answer
3. Empty — the model refuses to answer without context
4. Identical to the RAG version

## Question 3: Token usage — short summary
Run 4_simple_agent.yaml with summary_length = short (leave the other inputs as defaults).

Open the execution logs and find the token usage logged by the log_token_usage task.

What is the approximate output token count for multilingual_agent?

1. 5-15 tokens
2. 60-100 tokens <-- answer
3. 200-400 tokens
4. 500+ tokens

### The Kestra Flow and Process to initiate the kestra  - 
1. Create a Docker.yml file 
2. Obtain the Gemini API key —
Visit Google AI Studio and generate a free API key. This key is required for AI Copilot and agent-based flows (GEMINI_API_KEY).

3. Start Kestra locally —
Run the following command in your terminal:
<img width="614" height="161" alt="Screenshot 2026-07-03 at 21 20 31" src="https://github.com/user-attachments/assets/f8db82a9-f3d5-4a2a-a2d0-6fb3db9cd0bc" />



4. Open the Kestra UI and log in —

   Navigate to http://localhost:8080 in your browser.

   <img width="1146" height="422" alt="Screenshot 2026-07-03 at 21 21 19" src="https://github.com/user-attachments/assets/fc04b9a9-3c15-4cb9-a978-69d85de8eec2" />




In local (open-source) Kestra, the UI opens directly without a login screen by default.



The command in Step 4 automatically reads the key from your local environment (e.g., .zshrc) and passes it into Kestra as a base64-encoded secret.
Import the homework flows —

5.Import the Flows from your local computer to the Kestra by using following command

cd 03-orchestration

# Adjust username and password to match your Kestra setup
curl -X POST -u 'admin@kestra.io:Admin1234!' http://localhost:8080/api/v1/flows/import -F fileUpload=@flows/1_chat_without_rag.yaml
curl -X POST -u 'admin@kestra.io:Admin1234!' http://localhost:8080/api/v1/flows/import -F fileUpload=@flows/2_chat_with_rag.yaml
curl -X POST -u 'admin@kestra.io:Admin1234!' http://localhost:8080/api/v1/flows/import -F fileUpload=@flows/3_rag_with_websearch.yaml
curl -X POST -u 'admin@kestra.io:Admin1234!' http://localhost:8080/api/v1/flows/import -F fileUpload=@flows/4_simple_agent.yaml
curl -X POST -u 'admin@kestra.io:Admin1234!' http://localhost:8080/api/v1/flows/import -F fileUpload=@flows/5_web_research_agent.yaml
curl -X POST -u 'admin@kestra.io:Admin1234!' http://localhost:8080/api/v1/flows/import -F fileUpload=@flows/6_multi_agent_research.yaml

6. Execute a flow —
7. 
Open the desired flow, click Execute, provide any required inputs  and run it. Then check the Logs tab of the execution to view outputs such as log_token_usage.


### Output

## <img width="1146" height="422" alt="Screenshot 2026-07-03 at 21 32 20" src="https://github.com/user-attachments/assets/869f74b8-9c2a-49db-aff1-15933848822d" />
Question 1

✅ AI Copilot has access to current Kestra plugin documentation

Explanation:
Kestra AI Copilot produces better and more accurate flows because it is grounded in the latest Kestra-specific context, including up-to-date plugin names, task types, and official syntax from Kestra’s documentation.

General ChatGPT may generate plausible workflows, but it can:

Use outdated or incorrect plugin names
Miss recent Kestra updates
Hallucinate task types that don’t exist

In contrast, AI Copilot is integrated with Kestra’s internal knowledge base, so it:

Knows the exact current plugin structure
Uses valid task definitions (io.kestra.plugin.gcp.bigquery.Load, etc.)
Produces production-ready YAML aligned with Kestra’s ecosystem

That’s why the flows from Copilot are typically more reliable and immediately executable.

## Question 2

✅ Vague, generic, or fabricated — the model guesses from training data

Explanation:
In the non-RAG flow (1_chat_without_rag.yaml), the model does not have access to external documents or Kestra documentation. It relies only on its internal training data, which may be:

Outdated
Incomplete
Not specific to Kestra 1.1 release notes

As a result, the response typically becomes:

Generalized (e.g., “improved performance”, “bug fixes”)
Not grounded in actual Kestra 1.1 documentation
Sometimes partially hallucinated or inaccurate

In contrast, the RAG flow (2_chat_with_rag.yaml) retrieves real context from documentation before generating the answer, making it:

More precise
Fact-based
Aligned with actual release notes

So the key difference is grounded context vs. model guesswork.


## Question 3
INFO 2026-07-03T19:31:48.766854Z 📊 Token Usage Summary:

Multilingual Agent:
- Input tokens: 282
- Output tokens: 83
- Total tokens: 365

English Brevity Agent:
- Input tokens: 98
- Output tokens: 38
- Total tokens: 136

💡 Tip: Monitor token usage to understand costs and optimize prompts!


<img width="1169" height="522" alt="Screenshot 2026-07-03 at 21 34 26" src="https://github.com/user-attachments/assets/97174129-6089-4d2a-81b1-35a8a9bcf87b" />


## Question 4: Token usage — long summary
Run 4_simple_agent.yaml again with summary_length = long.

Compare the multilingual_agent output token count to your result from Question 3. Roughly how many times more output tokens does the long summary use?

1. About the same (within 20%)
2. 2-5x more <-- answer
3. 10-20x more
4. 50x more

### Output - 

<img width="1169" height="522" alt="Screenshot 2026-07-03 at 21 36 13" src="https://github.com/user-attachments/assets/573993a1-c17e-479d-9de3-ff01dd91d2b4" />


INFO 2026-07-03T19:37:49.873999Z 📊 Token Usage Summary:

Multilingual Agent:
- Input tokens: 282
- Output tokens: 169
- Total tokens: 451

English Brevity Agent:
- Input tokens: 184
- Output tokens: 43
- Total tokens: 227

💡 Tip: Monitor token usage to understand costs and optimize prompts!

```

Reasoning:
✅ About 2–5x more

When I compared the token usage between the short and long summaries, I found that the long summary used significantly more output tokens.

In Question 3 (short summary), the Multilingual Agent used 83 output tokens, while in Question 4 (long summary), it used 169 output tokens. This is roughly 2 times more tokens.

This increase happens because the long summary includes more detailed explanations and additional sentences, which naturally requires more tokens to generate.Therefore, the correct choice is “2–5x more”, since the long version clearly uses more tokens than the short version, even though in this case it is closest to about 2x.





## Question 5: Modifying a flow

Open 4_simple_agent.yaml in the Kestra flow editor. Find the english_brevity task and change its prompt from asking for exactly 1 sentence to asking for exactly 3 sentences.

Save the flow, then run it with summary_length = long.

Compare the english_brevity output token count to the original 1-sentence version (also with summary_length = long). How do they compare?

1. About the same (within 20%) <-- answer
2. 2-4x more
3. 5-10x more
4. 10x+ more

### Output

INFO 2026-07-03T19:45:24.792546Z 📊 Token Usage Summary:

Multilingual Agent:
- Input tokens: 282
- Output tokens: 203
- Total tokens: 485

English Brevity Agent:
- Input tokens: 218
- Output tokens: 88
- Total tokens: 306

💡 Tip: Monitor token usage to understand costs and optimize prompts!

Answer and Reasoning:

 2–4x more

After modifying the english_brevity task to generate exactly 3 sentences instead of 1 sentence and running the flow with summary_length = long, I observed an increase in the output token count.

In the original run (1 sentence), the English Brevity Agent used 43 output tokens. After changing the prompt to generate 3 sentences, it used 88 output tokens.

This is approximately:

88÷43≈2.05

or about 2 times more output tokens.

The increase is expected because generating three sentences requires the model to produce more content than a single sentence. As a result, the output token count increases proportionally.

## Question 6: Best Practices

Based on what you learned in this module, for production workflows requiring deterministic, repeatable results with strict compliance requirements (e.g., financial reporting, workflows in highly regulated industries), which approach is most appropriate?

1. Always use AI agents for maximum flexibility and adaptation
2. Use traditional task-based workflows for predictability and auditability <-- answer
3. Use only RAG without agents for better performance
4. Use web search tools exclusively to ensure current data

Reasoning:

✅ Use traditional task-based workflows for predictability and auditability

Explanation:
For production systems in highly regulated or compliance-heavy environments (such as finance, healthcare, or legal workflows), the most important requirements are determinism, repeatability, and auditability.

Traditional task-based workflows (like structured Kestra flows) are preferred because they:

Produce consistent, repeatable outputs
-Are easy to trace and debug step-by-step
-Provide clear execution logs for auditing
-Do not introduce randomness or variability like AI agents might

In contrast:

-AI agents add flexibility but reduce determinism
-RAG improves context but still depends on LLM generation variability
-Web search introduces external uncertainty and inconsistency

Therefore, for strict compliance use cases, structured workflow orchestration is the safest and most reliable approach

