🚀 Project Overview
In today’s fast-paced talent landscape, manually sourcing, screening, and ranking candidates is labor-intensive, prone to human bias, and inefficient. This project presents a robust AI-powered pipeline that automates candidate evaluation and dynamically adapts to human feedback. By leveraging Large Language Models (LLMs) like Gemma 3, GROK, and Qwen3 fine-tuned with LoRA via Unsloth, we significantly streamline candidate scoring and ranking based on role-specific fitness.

📌 Problem Statement
Our talent sourcing operation faces multiple pain points:

Manual Review Bottlenecks: Recruiters spend considerable time evaluating unranked candidates.

Subjective Ranking: Top-fit candidates are not always at the top due to lack of automation.

Unstructured Profiles: Profiles vary in structure and content, complicating keyword-based screening.

Bias Risks: Manual reviews can inadvertently introduce subjective bias.

🎯 Project Goals
Automate candidate fitness evaluation using AI-generated scores.

Rank candidates based on semantic understanding of job roles, not just keywords.

Re-rank the list when a candidate is starred, using that as supervisory feedback.

Establish a cutoff score to filter out low-fit candidates.

Explore techniques to reduce human bias through ML-assisted assessments.

🔄 Project Pipeline
1. 🧹 Data Preprocessing
Candidate profiles are collected from a proprietary sourcing pipeline.

Each profile is de-identified and structured with:

id

job_title

location

connections

A candidate profile string is generated to consolidate relevant attributes into a single text prompt.

2. 🧠 Candidate Scoring with LLMs
We experimented with three models using Unsloth + LoRA:

Method 1: Gemma 3 4B
Fine-tuned using LoRA for efficient scoring.

Scoring prompt: Acts like an expert recruiter, assigning a score from 1 to 10 for a given role.

Extracts score using deterministic decoding.

Method 2: GROK-1
Built on Mistral-7B using LoRA.

Memory-efficient and capable of understanding complex semantic cues.

Used for broader roles with more generalizable prompts.

Method 3: Qwen3 (Qwen1.5-4B-Instruct)
Scoring includes pre-filtering based on search terms like "aspiring".

Ensures non-relevant candidates (e.g., unrelated industries) get filtered early with a score of 0.

3. 📈 Ranking Candidates
Scores generated from the LLM are used to sort candidates descendingly.

Profiles with high semantic alignment to the job title (e.g., “HR Manager”, “People Development Specialist”) receive higher scores.

Outliers (e.g., “Software Engineer” with no HR experience) are down-ranked or scored 0.

4. ⭐ Re-Ranking via Human Feedback
Recruiters can “star” a candidate during manual review.

Starred candidate becomes a supervisory signal for ideal profile.

The pipeline re-evaluates all candidates, adjusting scores based on similarity to the starred profile using either:

Embedding similarity

Reinforcement fine-tuning (future work)

5. 🔍 Filtering Low-Fit Candidates
Candidates scoring below a cutoff threshold (e.g., score < 3) are filtered out automatically.

Thresholds can be role-specific or generalized via clustering across roles.

📊 Sample Output Snapshot
ID	Job Title	Location	Connections	Score (Gemma)
01	Aspiring HR Professional	London	500+	8
02	People Development Specialist	San Francisco	500+	9
03	Student – No HR Role Mentioned	Remote	150	2
04	Engineering Manager	New York	500+	0

💡 Key Insights
LLM Scoring Beats Keyword Matching: Models can infer intent and potential from aspirational language (e.g., "aspiring", "seeking HR").

Dynamic Feedback = Better Recommendations: As more candidates are starred, the system fine-tunes future rankings.

Cutoff Scores Enable Bulk Filtering: We can confidently eliminate irrelevant candidates early, improving focus.

🧠 Ideas for Future Automation
Reinforcement Learning from Human Feedback (RLHF): To continuously adapt to reviewer preferences.

Embedding-Based Similarity Matching: To re-rank based on profile closeness to starred candidates.

Bias Audits: Identify scoring imbalances across demographics or regions.

🏁 Conclusion
This project showcases a scalable, AI-driven pipeline to transform the candidate screening and ranking process. By blending machine intelligence with human oversight, we deliver:

Faster shortlisting

Smarter filtering

Adaptable rankings

Reduced bias

Our system empowers hiring managers and recruiters to focus on strategic hiring decisions, not manual screening.
