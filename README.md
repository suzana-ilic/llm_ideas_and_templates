# LLM Ideas and Templates
Ideas and templates for Prompt Engineering, Synthetic Dataset Generation, Guidelines, Data Labeling, etc.

# A Practical Playbook for Synthetic Data Generation

This playbook provides a comprehensive and practical guide for generating high-quality synthetic data. It is designed for data scientists, ML engineers, prompt engineers and domain experts who need to train, fine-tune, or evaluate LLMs when real-world data is unavailable, private, or insufficient.

**Domains Covered:**
* Language & Communication
* Tech & Digital Products
* Security & Privacy
* Retail & E-Commerce
* Enterprise & Workflows
* Education

---

## A Practical Workflow for Synthetic Data Generation

Creating high-quality synthetic data is a structured, iterative process. Follow these steps for reliable and effective dataset generation.

### Step 1: Define the Task and a Strict Schema
Before writing a single prompt, clearly define your model's target task and the exact data structure it requires. A strict schema is the foundation for clean, usable data.

* **Example Schema for an Email Triage Task:**

| Field Name     | Data Type | Description                                          | Example                               |
| :------------- | :-------- | :--------------------------------------------------- | :------------------------------------ |
| `message_id`   | `string`  | A unique identifier for the data point.              | `email-syn-001`                       |
| `body`         | `string`  | The full text content of the email.                  | "Hi team, the server is down..."      |
| `subject`      | `string`  | The email subject line.                              | "URGENT: Server Outage"               |
| `urgency`      | `string`  | A classification label from a controlled taxonomy.   | `High`                                |
| `category`     | `string`  | The department or issue type for routing.            | `IT_Support`                          |
| `metadata`     | `dict`    | Additional context like timestamps or user roles.    | `{"sender_role": "Manager"}`          |

### Step 2: Develop Parameterized Prompt Templates
Don't use static, one-off prompts. Create robust templates with placeholders that can be programmatically filled. This is the key to generating diversity and scale.

* **Before (Static Prompt):**
    > "Write an urgent email about a server being down."

* **After (Parameterized Prompt Template):**
    > You are a `{sender_role}` at a mid-sized tech company. Write an email to the `{recipient_team}` team with the subject line `"{subject}"`. The email should have a `{tone}` tone and report the following issue: `{issue_description}`. Ensure the urgency is clearly communicated.

    * **Variables:** `{sender_role}`, `{recipient_team}`, `{subject}`, `{tone}`, `{issue_description}`

### Step 3: Source and Inject Variation
To avoid a monotonous dataset, programmatically inject variety into your prompt templates.

* **Create Lists of Variables:** Maintain lists or files of potential values for your template placeholders (e.g., a list of 100 product names, 20 sender roles, 5 tones).
* **Introduce Realistic Noise:** Real data is imperfect. Write small helper functions to programmatically introduce common errors:
    * Typographical errors (`"teh"` instead of `"the"`)
    * Varied phrasing (`"can you help?"`, `"need assistance"`, `"I'm stuck"`)
    * Variations in formality (slang, jargon, professional language)
* **Rotate Personas:** Systematically vary the persona of the generator to capture different viewpoints (e.g., frustrated customer, curious new user, technical expert).

### Step 4: Generate in Batches and Validate
While you can generate data manually directly in a playground, you can also generate data in batches using APIs or scripts for a more automated and scalable approach. After each batch, perform validation.

* **Automated Validation:** Write scripts to check if every generated sample conforms to the schema defined in Step 1. Reject any malformed outputs.
* **LLM-based Validation:** Use a second, "evaluator" LLM to check the quality of the generated data. Ask it questions like: "On a scale of 1-5, how realistic is this customer support chat?" or "Does this text contain PII? Answer with only 'Yes' or 'No'."
* **Human-in-the-Loop Review:** No automated process is perfect. Have a human spot-check a small percentage of each batch to catch subtle errors, biases, or unrealistic patterns the models might miss.

### Step 5: Analyze, Refine, and Iterate
Treat dataset generation as an iterative project. Analyze your generated data. Are the labels balanced? Is there enough diversity? Use your findings from the validation step to refine your prompt templates, add more variation sources, and generate a new, improved batch.

---

## Common Pitfalls and How to Avoid Them

* **Pitfall: Generator Collapse.** The LLM starts producing repetitive or very similar examples.
    * **How to Avoid:** Aggressively vary your prompt templates. Use a higher `temperature` setting during generation to encourage creativity. Ensure your source lists for variables (Step 3) are large and diverse.
* **Pitfall: Unrealistic Perfection.** The synthetic data is too clean (perfect grammar, no slang), so the model fails on messy, real-world inputs.
    * **How to Avoid:** Intentionally inject noise (Step 3). Prompt the LLM to use a specific, imperfect persona (e.g., "You are a busy user typing on a mobile phone").
* **Pitfall: Forgetting the "Negative Class".** You generate many examples of what to detect (e.g., toxic comments) but no examples of what to ignore (e.g., nuanced, safe criticism). This leads to a trigger-happy model.
    * **How to Avoid:** For every class you want to model, explicitly generate a "negative" or "benign" class. For PII detection, generate examples of text that *looks like* PII but isn't (e.g., order numbers, generic IDs).
* **Pitfall: Data Contamination.** Be careful that your synthetic data doesn't accidentally mirror the LLM's own training data too closely, which can lead to models that perform well on your synthetic set but fail to generalize.
    * **How to Avoid:** Source your own unique seed data for prompts where possible. Always test the final model on a holdout set of *real* human-generated data, even if it's small.

---

## 🌐 Language & Communication

### Intent Classification & Slot Filling
Generate user queries directed at a conversational AI across various domains (e.g., booking flights, ordering food, checking weather). Each query is crafted to test a specific intent and contains entities (slots) to be extracted.

* **Metadata:** Domain (e.g., Travel, Food Service), User Persona (e.g., Novice, Power User), Channel (e.g., Mobile App, Smart Speaker).
* **Labels:** Intent (e.g., `BookFlight`), Slots and Values (e.g., `{"destination": "Tokyo", "date": "2025-10-15"})`.
* **Primary Use Cases:** Training NLU models, building task-oriented chatbots, and evaluating dialogue systems.
* **Real-World Pro-Tip:** Generate ambiguous queries that could match multiple intents to train your model's disambiguation and clarification logic (e.g., "Book a table" could be for a restaurant or a library).

### Complex Instruction Following
A dataset of multi-step, conditional, or abstract instructions. Examples range from technical procedures to creative tasks.

* **Metadata:** Task Complexity (1-5), Domain (e.g., Technical, Creative), Number of Steps.
* **Labels:** Instruction Text, Expected Output/Action Sequence, Ambiguity Flags.
* **Primary Use Cases:** Training agentic models, improving instruction-following capabilities, and testing logical reasoning.
* **Real-World Pro-Tip:** Include "exception" steps in your instructions (e.g., "If the file doesn't exist, create it first, then..."). This tests the model's ability to handle conditional logic, a common failure point.

---

## 💻 Tech & Digital Products

### Code Generation & Explanation
Generate code snippets in various programming languages based on natural language descriptions. Include corresponding explanations of what the code does, its complexity, and potential edge cases.

* **Metadata:** Programming Language, Library/Framework (e.g., React, Pandas), Difficulty (Beginner to Expert).
* **Labels:** Natural Language Prompt, Generated Code, Code Explanation, Big-O Complexity.
* **Primary Use Cases:** Training code generation models, building developer assistant tools, and powering educational coding platforms.
* **Real-World Pro-Tip:** Generate prompts that ask the model to *refactor* or *debug* existing (intentionally flawed) code, not just generate new code. This is a more challenging and valuable real-world skill.

### User Interface (UI/UX) Feedback Analysis
A collection of user feedback on digital products, ranging from bug reports to feature requests and general impressions.

* **Metadata:** Product Area (e.g., Onboarding, Checkout), Device (Desktop, iOS), User Segment (e.g., New User, Admin).
* **Labels:** Feedback Text, Sentiment (Positive, Negative, Neutral), Category (Bug, Feature Request, Usability), Actionability Score.
* **Primary Use Cases:** Automating feedback triage, summarizing user sentiment, and identifying product improvement opportunities.
* **Real-World Pro-Tip:** Generate feedback that mixes categories (e.g., a single comment that praises one feature but reports a bug in another). This tests the model's ability to perform multi-label classification.

---

## 🔐 Security & Privacy

### Anonymized Conversations with PII
Conversations containing synthetic Personally Identifiable Information (PII) like names, emails, and credit card numbers.

* **Metadata:** Conversation Domain (e.g., Healthcare, Finance), Anonymization Technique.
* **Labels:** Labeled spans for each PII type (e.g., `[PERSON]`, `[EMAIL]`), Original Text, Redacted Text.
* **Primary Use Cases:** Training PII detection and redaction models, evaluating data loss prevention (DLP) systems.
* **Real-World Pro-Tip:** Your dataset is incomplete without "near-misses." Generate examples that look like PII but aren't (e.g., order IDs formatted like credit cards, user-generated names that are dictionary words). This is crucial for reducing false positives.

### Security Incident Reports
Narrative summaries of simulated cybersecurity events, including phishing attacks, malware detection, and system access violations.

* **Metadata:** Incident Type, Severity Level (1-5), Affected Systems, Timestamp of Events.
* **Labels:** Incident Summary, MITRE ATT&CK Tactic/Technique, Indicators of Compromise (IOCs), Recommended Actions.
* **Primary Use Cases:** Training models for security orchestration and automated response (SOAR), red teaming LLMs, and summarizing threat intelligence.
* **Real-World Pro-Tip:** Use a real, public threat intelligence feed (like a security blog RSS) to seed the `{issue_description}` in your prompt template. This ensures your synthetic data reflects current, real-world attack vectors.

---

## 🛍️ Retail & E-Commerce

### Customer Product Reviews
Richly varied reviews across categories. Reviews are written in diverse tones (enthusiastic, frustrated, technical, humorous).

* **Metadata:** Product Category, Star Rating (1-5), Verified Purchase Status.
* **Labels:** Review Text, Sentiment (Positive, Negative, Mixed), Key Aspects Mentioned (e.g., Battery Life, Fabric Quality).
* **Primary Use Cases:** Fine-tuning sentiment analysis, generating realistic review summaries, and identifying product flaws.
* **Real-World Pro-Tip:** Don't generate a uniform distribution of star ratings. Model a realistic distribution (e.g., 60% 5-star, 15% 4-star, 5% 3-star, 5% 2-star, 15% 1-star) to prevent your model from being biased by unrealistic data balance.

### Customer Support Chats (Retail)
Simulated conversations about returns, shipping issues, product inquiries, and complaints. Chats demonstrate problem-solving workflows and de-escalation techniques.

* **Metadata:** Issue Type (e.g., `SHIPPING_DELAY`), Customer Status (e.g., New, VIP), Channel (Chat, Email).
* **Labels:** Roles (Agent, Customer), Dialogue Acts, Resolution Status, Customer Satisfaction (CSAT) Score.
* **Primary Use Cases:** Training retail chatbots, creating agent-assist tools, and automating support ticket summarization.
* **Real-World Pro-Tip:** Generate multi-turn conversations where the customer's issue *evolves* or they provide clarifying information later in the chat. This tests the model's ability to maintain context over a longer interaction.

---

## 🏢 Enterprise & Workflows

### Meeting Minutes and Action Items
Synthetic summaries of workplace meetings like team syncs, project kick-offs, and incident retrospectives.

* **Metadata:** Meeting Type, Department, Project Name, Participants.
* **Labels:** Discussion Highlights, Key Decisions, Assigned Tasks (with owner and due date), Meeting Summary.
* **Primary Use Cases:** Powering automated summarization tools, training enterprise productivity agents, and building task-tracking systems.
* **Real-World Pro-Tip:** Create linked series of meetings. For example, a "Project Kick-off" meeting summary, followed by a "Weekly Sync" summary that references decisions from the kick-off. This helps train models on longitudinal, project-based context.

### Internal Email Threads
Realistic email exchanges covering project updates, escalations, onboarding, and cross-team collaboration.

* **Metadata:** Subject Line, Timestamp, Participant Roles, Thread Length.
* **Labels:** Email Intent (e.g., Request, Inform, Escalate), Urgency Level, Conversation Topic, Summary.
* **Primary Use Cases:** Training smart reply models, developing email summarizers, and building automated email triage systems.
* **Real-World Pro-Tip:** Focus on generating realistic *threads*, not just single emails. Prompt the LLM to create a 4-email sequence with replies, forwards, and new people being added to the CC line. The context is in the thread, not the individual message.

---

## 📚 Education

### Classroom Dialogue Transcripts
Simulated classroom conversations capturing dynamic interactions between teachers, students, and parents across multiple subjects and grade levels.

* **Metadata:** Subject, Grade Level, Dialogue Setting (e.g., One-on-One, Group Work).
* **Labels:** Dialogue Acts (e.g., Question, Clarification), Participant Roles, Action Items, Summaries.
* **Primary Use Cases:** Training AI tutors, fine-tuning summarization models for educational content, and developing classroom analytics tools.
* **Real-World Pro-Tip:** Generate dialogues that contain common misconceptions about a topic (e.g., a student incorrectly explaining photosynthesis). This allows you to train an AI tutor not just to explain concepts, but to *identify and correct* misunderstandings.

### Student Essays and Reflections
Synthetic essays, book reports, and reflective journals written from a student’s perspective, showcasing varying writing quality and coherence.

* **Metadata:** Subject, Grade Level, Prompt Type (e.g., Argumentative, Narrative), Quality Score (1-5).
* **Labels:** Essay Text, Writing Purpose, Coherence Score, Grammatical Correctness.
* **Primary Use Cases:** Developing automated essay scoring systems, building writing assistance tools, and evaluating text coherence.
* **Real-World Pro-Tip:** Instruct the generator to write essays that fulfill the prompt but contain specific logical fallacies (e.g., "Straw Man," "Ad Hominem"). This can be used to train advanced writing assistants that provide feedback on argumentation, not just grammar.
