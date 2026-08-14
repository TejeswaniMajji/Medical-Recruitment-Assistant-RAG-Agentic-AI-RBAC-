
# Medical Recruitment Assistant

A secure, role-aware medical recruitment assistant integrating Retrieval-Augmented Generation (RAG) and Agentic AI with modern AI and backend technologies. Built with FastAPI, MongoDB, Pinecone, LangChain, and LangGraph, this system automates the hiring process for healthcare roles, ensuring role-specific access for users like recruiters, hiring managers, and candidates.

Developed and maintained by Pavan Kumar Eleti.

## Project Overview

This project delivers an AI-driven recruitment assistant tailored for the healthcare domain. It combines Generative AI for content creation (e.g., job descriptions, offer letters) and Agentic AI for autonomous task execution (e.g., posting jobs, scheduling interviews). The system uses Large Language Models (LLMs) with vector databases and role-based access control (RBAC) to provide intelligent, secure, and role-sensitive responses.

- RBAC Integration ensures sensitive information is shared appropriately
- Supports roles: Recruiter, Hiring Manager, Candidate, Guest
- Built for scalability, modularity, and healthcare recruitment efficiency

## Application Architecture

![Application Flow](./assets/applicationFlow.png)

## Core Modules

![Core Modules](./assets/coreModules.png)

[View Full Project Report (PDF)](./assets/projectReport.pdf)

## Live Demo

- Frontend (Streamlit): [rbac-medicalassistant](https://rbac-medicalassistant-vbs9bxxzjfnpab6dsrfwah.streamlit.app/)
- Backend (Render): [FastAPI Server](https://rbac-medicalassistant.onrender.com)

## Tech Stack

| Layer        | Technology                                |
|--------------|------------------------------------------|
| Backend      | FastAPI (modular design)                 |
| Database     | MongoDB Atlas (user authentication, RBAC)|
| Vector Store | Pinecone (document embeddings & search)  |
| LLM          | LLaMA-3 via Groq API                     |
| Embeddings   | Google Generative AI Embeddings          |
| Auth         | HTTP Basic Auth with bcrypt              |
| Frontend     | Streamlit (optional for demo)            |
| Workflow     | LangChain (RAG workflows), LangGraph (Agentic workflows) |

## Directory Structure

| Directory    | Purpose                                                  |
|--------------|---------------------------------------------------------|
| auth/        | Signup/Login logic, password hashing                     |
| chat/        | Handles RAG-based Q&A flow                              |
| vectordb/    | Chunking, indexing, and interaction with Pinecone       |
| database/    | MongoDB user schema, roles, operations                  |
| main.py      | FastAPI entry point, route orchestration                |
| agent/       | LangGraph-based agentic workflows for hiring automation  |

## Role-Based Access Control (RBAC)

| Role           | Permissions                                                  |
|----------------|-------------------------------------------------------------|
| Recruiter      | Uploads job descriptions, manages candidate shortlisting, schedules interviews |
| Hiring Manager | Access to candidate resumes and interview schedules         |
| Candidate      | General job-related queries, application status (restricted access) |
| Guest          | Public job information only (minimal access)                |

## API Endpoints

| Method | Endpoint        | Description                          |
|--------|-----------------|--------------------------------------|
| POST   | /signup         | Register a new user                  |
| GET    | /login          | Login using Basic Auth               |
| POST   | /upload_docs    | Recruiter-only: Upload job-related documents |
| POST   | /chat           | Role-restricted Q&A for recruitment queries |
| POST   | /post_job       | Recruiter-only: Post job to platforms |
| POST   | /schedule       | Recruiter-only: Schedule interviews  |
| POST   | /send_offer     | Recruiter-only: Generate and send offer letters |

## Automated Hiring Workflow

The assistant automates the hiring process for roles like backend engineers in healthcare:

1. **Creating a Job Description (JD)**:
   - Uses Generative AI to draft JDs based on templates, internal salary bands, or high-performing examples (e.g., for a backend engineer with 2-4 years of experience in Java, Python, or C++).
2. **Posting the JD**:
   - Agentic AI posts JDs to platforms like LinkedIn or GitHub using APIs.
3. **Shortlisting**:
   - RAG-based system retrieves and evaluates applications using resume parsers and internal criteria.
4. **Interviewing**:
   - Generates role-specific questions (e.g., "How to scale a backend system for high traffic?") and schedules interviews via calendar APIs.
5. **Rolling an Offer Letter**:
   - Generates and sends offer letters using mail APIs.
6. **Onboarding**:
   - Provides welcome emails, policies, and checklists for new hires.

## Getting Started

1. **Clone the Repository**

   ```bash
   git clone https://github.com/pavankumareleti/rbac-medicalAssistant.git
   cd rbac-medicalAssistant
   ```

2. **Create Environment Variables**

   Create a `.env` file with your configuration:

   ```env
   MONGO_URI=your_mongo_uri
   DB_NAME=your_db_name
   PINECONE_API_KEY=your_pinecone_key
   GOOGLE_API_KEY=your_google_api_key
   GROQ_API_KEY=your_groq_key
   ```

3. **Set Up Virtual Environment**

   ```bash
   uv venv
   .venv/Scripts/activate  # On Windows
   source .venv/bin/activate  # On macOS/Linux
   ```

4. **Install Dependencies**

   ```bash
   uv pip install -r requirements.txt
   ```

5. **Run the Server**

   ```bash
   uvicorn main:app --reload
   ```

## Planned Improvements

- Implement JWT-based authentication with refresh tokens
- Develop a React-based dynamic frontend
- Enable document preview and download functionality
- Add audit logs for recruitment compliance
- Expand role granularity for finer access control
- Optimize embeddings and agentic workflow performance
- Integrate additional hiring platforms (e.g., Indeed, AngelList)

## Generative and Agentic AI Details

### Generative AI
- **Purpose**: Creates content like job descriptions, offer letters, and interview questions by learning data distributions.
- **Use Cases**: Drafting JDs, generating onboarding materials, and providing general recruitment advice.
- **Challenges**: Reactive, lacks memory, cannot take actions, and provides generic responses.

### Agentic AI
- **Purpose**: Autonomously pursues recruitment goals (e.g., posting jobs, scheduling) with planning, reasoning, and context awareness.
- **Key Characteristics**:
  - **Autonomy**: Executes tasks like posting JDs or scheduling interviews independently.
  - **Goal-Oriented**: Breaks down goals (e.g., hiring a backend engineer) into actionable steps.
  - **Planning**: Generates and selects optimal plans (e.g., LinkedIn vs. internal referrals).
  - **Reasoning**: Handles errors (e.g., failed API calls) and adapts to feedback (e.g., low application numbers).
  - **Context Awareness**: Retains task history, user preferences, and API responses for informed decisions.
- **Tools**: LinkedIn API, resume parsers, calendar APIs, mail APIs, and HRM access tools.

## LangChain and LangGraph Integration

- **LangChain**:
  - Used for RAG-based workflows, such as retrieving relevant job applications or generating responses based on stored documents.
  - Suitable for simple conversational tasks like answering candidate queries.
- **LangGraph**:
  - Powers complex, non-linear agentic workflows (e.g., hiring pipeline with conditional paths and loops).
  - Manages state (e.g., tracking application status) and supports event-driven execution.
- **When to Use**:
  - LangChain: For straightforward prompt-based or retrieval tasks.
  - LangGraph: For stateful, multi-step workflows with conditional logic and tool integration.

## Contributing

Contributions are welcome! To contribute:

1. Fork the repository
2. Create a feature branch
3. Submit a pull request with detailed changes

## Author

Pavan Eleti  
Data Scientist  
Email: pavankumareleti@example.com  
GitHub: https://github.com/pavankumareleti  
LinkedIn: https://linkedin.com/in/pavankumareleti  

© 2025 Pavan Kumar Eleti — All rights reserved.
```
