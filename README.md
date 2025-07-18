# LLM Ideas and Templates
Ideas and templates for Prompt Engineering, Synthetic Dataset Generation, Guidelines, Data Labeling, etc.

# Synthetic Dataset Generation

A collection of practical, real-world ideas for synthetic dataset generation across 
- Language & Communication,
- Security & Privacy,
- Retail & E-Commerce,
- Enterprise & Workflows,
- Tech & Digital Products,
- and Education.

Designed for training and evaluating language models in scenarios where real data is unavailable, costly, or sensitive.

## 🔧 General Instructions for Synthetic Dataset Generation

To generate high-quality, realistic, and diverse synthetic datasets:

- **Define a Schema**: Outline the fields and structure of each dataset (e.g., text, category, metadata).
- **Create Controlled Taxonomies**: Design consistent categories, tags, and labels for classification tasks.
- **Write Prompt Templates**: Use prompt engineering with variations in tone, structure, and domain.
- **Include Context & Metadata**: Add metadata (e.g., role, timestamp, product category, urgency).
- **Introduce Natural Noise**: Incorporate typos, grammar errors, or informal speech patterns when realistic.
- **Ensure Diversity**: Vary domain, demographics, and linguistic style.
- **Include Labeled and Unlabeled Samples**: Provide both for supervised and unsupervised training.

---

## 📚 Education

### Classroom Dialogue Transcripts

Simulated classroom conversations across grade levels and subjects. Dialogues include conceptual Q&A, clarification exchanges, group discussions, and parent-teacher meetings. Each sample contains role-labeled utterances (e.g., teacher, student, parent), along with metadata like subject and grade. Labeled for dialogue acts, participant roles, and action items. Useful for summarization, tutoring, and AI teacher tools.

### Homework Assignment Instructions

A diverse collection of homework prompts across subjects and assignment types. Includes creative writing, math word problems, reading comprehension tasks, and science experiment guides. Metadata includes subject, grade level, estimated duration, and rubric criteria. Supports instructional content generation and assignment comprehension tasks.

### Student Essays and Reflections

Synthetic essays and narratives written from a student’s perspective. Includes opinion pieces, book reports, reflective essays, and argumentative texts. Varying in writing quality, tone, and coherence across grades. Metadata includes subject, prompt type, and writing purpose. Useful for writing assistance tools and essay scoring models.

### Tutoring Q&A Sessions

Simulated one-on-one tutoring dialogues across subjects such as math, writing, and science. Includes conceptual explanations, study tips, clarifying questions, and practice problem walkthroughs. Metadata includes academic level, tutor role, question complexity, and topic area. Enables fine-tuning of AI tutors and study assistants.

### Educational App Reviews

User reviews from students, teachers, and parents describing educational software. Feedback covers usability, outcomes, engagement, and design. Each review includes metadata like reviewer type, age group, rating (1–5), and sentiment. Ideal for sentiment analysis, review summarization, and educational UX evaluation.

---

## 🏢 Enterprise & Workflows

### HR Interview Conversations

Structured interview Q&A logs for roles across domains. Includes behavioral questions, technical screens, culture-fit discussions, and follow-up communications. Annotated with interviewer/interviewee roles, job type, interview stage, and evaluation scores. Labeled for question type, candidate sentiment, and evaluation summary.

### Meeting Minutes and Action Items

Synthetic summaries of workplace meetings such as team syncs, retrospectives, and planning sessions. Each record includes topic, participants, goals, discussion highlights, and follow-up actions. Labels include assigned tasks, key decisions, and meeting type. Ideal for summarization tools and enterprise productivity agents.

### Internal Email Threads

Professional email exchanges for topics like project updates, escalations, onboarding, and cross-team coordination. Threads include subject lines, timestamps, participant metadata, and tone variation (formal, casual, urgent). Labels cover email intent, urgency, and conversation type. Supports summarization, smart reply, and thread classification.

### Helpdesk Ticket Logs

Structured helpdesk interactions on IT, HR, facilities, and software issues. Each entry includes user queries, ticket category, urgency, resolution notes, and satisfaction rating. Labels include ticket type, department, and sentiment. Ideal for building internal support agents and automated triage systems.

### Performance Review Comments

Short-form and narrative feedback from managers, peers, and self-assessments. Covers skills, accomplishments, growth areas, and promotion recommendations. Metadata includes role, review type, tone, and evaluation domain. Labeled for feedback category, sentiment, and impact level. Useful for performance tools and automated review generation.

---

## 🛍️ Retail & E-Commerce

### Customer Product Reviews

Richly varied reviews across product categories like electronics, fashion, and home goods. Includes star rating, review text, metadata (category, verified purchase, user profile), and sentiment labels. Written in diverse tones (enthusiastic, frustrated, humorous, neutral). Ideal for sentiment modeling, review generation, and summarization.

### Shopping Cart Events and Abandonment

Structured user sessions showing cart actions: product views, additions, removals, coupon use, and abandonment. Metadata includes device type, cart value, product categories, and session duration. Labels include event type, user status, and completion outcome. Useful for dropout prediction and purchase modeling.

### Customer Support Chats (Retail)

Simulated conversations between customers and support agents. Topics include returns, shipping issues, product questions, and complaints. Each chat includes roles, timestamps, topic classification, resolution status, and sentiment. Enables training for retail chatbots and summarizers.

### Product Descriptions with Structured Tags

Natural language product listings enriched with structured tags (e.g., size, color, material, season, brand tone). Covers categories like clothing, electronics, and furniture. Metadata includes product ID, description tone (minimalist, luxury, playful). Useful for training tagging models and recommender systems.

### Return Reason Logs

Freeform customer-provided reasons for returning products. Includes structured return metadata (product, window, return type), and natural language justifications (e.g., "arrived too late," "not as described"). Labels include reason category and customer sentiment. Valuable for reducing return rates and automating triage.

---

## 🔐 Security & Privacy

### Anonymized Chat Conversations with PII

Conversations containing synthetic personal information like names, emails, addresses, or phone numbers. Scenarios include customer service, medical advice, or casual messages. Labeled spans for PII types. Useful for training PII detection, redaction, and privacy-preserving NLP systems.

### Login Attempt Logs

Structured logs of successful and failed login attempts, with metadata like IP address, location, device, method (password, 2FA), and outcome. Includes suspicious patterns like geo-anomalies or brute-force attempts. Labels cover risk level, action taken (lockout, alert), and authentication success.

### Fake Identity Profiles

Complete synthetic user personas with names, demographics, education, job history, and contact info. Variations include fraudulent vs valid identities. Labels include authenticity, fraud likelihood, and identity completeness. Applicable in fraud detection and identity verification systems.

### Data Classification for Sensitive Info

Documents tagged by sensitivity level (e.g., public, internal, confidential, restricted). Types include financial reports, HR files, legal docs, and product roadmaps. Each document has topic metadata, file type, and department. Useful for document classification, access control, and governance.

### Security Incident Reports

Narrative-style summaries of simulated cybersecurity events. Includes phishing reports, malware detections, access violations, and IT team responses. Each entry contains incident type, severity level, affected systems, and resolution status. Labels include urgency, incident type, and follow-up requirements. Ideal for red teaming and incident response automation.

