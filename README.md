# Sean-Hilton-AI-for-Programmers-Final-Project
README file contains Final Project Memo based on Option 2

# Q&A Interview Assisting Tool (QAIAT)

*If your capacity allows, please share any practical feedback on the proposal that you believe would support this idea or raise my awareness of existing solutions.*

*Thank you to the Section Team for sharing your content & expertise.*

## Project Overview

### Description of Core Idea

The current state of non-AI-assisted Question-and-Answer (Q&A) interviewing relies largely on the interviewer's own skills and interests in managing key interview elements, including but not limited to:

- Clarifying the intent of questions asked
- Asking follow-up questions to dig further into the meaning of labels or nuanced content
- Noting when the speaker appears to have avoided or misunderstood questions

With the consent of interviewers and interviewees, the Q&A Interview Assisting Tool is designed to actively support interview management in (near) real-time. This tool analyzes interview audio transcripts to help provide an intuitive basis for ensuring the Q&A discussion reflects a meaningful exchange and minimizes the likelihood of preventable miscommunications.

### Stakeholder Benefits

This tool will benefit key Q&A Interview stakeholders in the following ways:

#### Interviewers
- AI-enhanced interview format may attract interest from potential interviewees and audiences
- When used transparently and with consent (necessary conditions for licensing this product), AI support may provide interviewers with a responsive approach for handling dodged questions, proposing targeted follow-up questions, and seeking greater clarity throughout the interview, all ultimately at the interviewer's discretion
- May relieve performance pressure to have an AI assistant as backup for safeguarding interview quality

#### Interviewees
- If used transparently and with consent, the tool may relieve potential concerns regarding interviewer bias
- May give interviewees more agency in the interviewing process, if interviewee is consulted on how QAIAT is used
- Through validation testing with experts and audiences, we would aim to demonstrate that using QAIAT results in more engaging and meaningful conversations

#### Audience
- AI-enhanced interview format may attract interest from audiences who enjoy interviews focused on deeper understanding
- Could train the QAIAT system based on audience preferences for seeking clarity and posing follow-up questions
- If used transparently, it may give audiences greater awareness of the decisions traditional interviewers implicitly make over the course of an interview, and how that impacts conversations

## Use Case & Workflow

### Beneficiary Personas
Q&A Interviewers such as:
- Podcasters
- Local Q&A event hosts
- Certain course instructors using Q&A for pedagogical purposes
- Certain therapists
- Certain recruiters

### Limitations
- Requires consenting participants
- Requires transparent implementation
- Requires audio feed, low-latency transcription, and low latency LLM analysis
- Requires experienced interviewers with training on integrating AI insights into discussion
- Requires secure, careful handling of any sensitive subject matter, both technically and interpersonally

### AI Improvement & Automation
- Automates (and may improve) semantic detection of disconnect between interview questions and answers
- Automates development of follow-up questions using (near) real-time transcript data
- When used with transparency and consent, QAIAT improves the experience of enforcing interview parameters (e.g., ensuring interview questions were answered directly), giving interviewers the ability to use AI analysis as supportive backing for such judgments

## AI Features to Be Implemented

### 1. Prompt Engineering

**Implementation:**
- Will be implemented to extract key details from transcripts
- Prompts will be organized in terms of:
  - **Categories** (types of information including "Question Meaning", "Response Relevance", "Jargon", etc.)
  - **Processing Chain** focusing on:
    1. Detection/Citation of the component in question (e.g., jargon terminology)
    2. Interpretation of the component within context of the interview at that point (e.g., highest probability definitions of the jargon)
    3. Recommendation of context-aware intervention designed to support interviewer (e.g., request confirmation that jargon meant X)

**Requirements:**
- Prompts must include details and examples that enable prioritization of transcript elements
- Must include variables that can be tailored to each specific interview (e.g., detection prompts may accept metadata and/or user inputs to indicate that scientific terms should be weighted more heavily for a certain interview, or to always exclude certain topics from analysis, or to return up to a certain number of terms based on the expected length of the interview)

**Justification:** Given the reliance of output on multi-layered LLM processes, the need to perform well in dynamic environments presented by structured interviews, the flexibility intended for the tool's use across topics and interview formats, and the need to gracefully handle the anticipated lag between the real-time conversation and the near real-time AI feedback, prompt engineering will be essential for this project.

### 2. Structured Outputs

**Implementation:**
- Examples to at least provide few shot training of the LLM will be used, conforming to the Categories and "Chain Layers" described in the prompt engineering section
- Structured Output from the LLMs will be standardized - perhaps as JSON output formats - and include prioritized detected elements, interpretations of such elements, and recommendations based on templates and prompts reviewed by interviewing experts

**Justification:** Because the system must be transparent to engender trust by all stakeholders, and to enhance reliability, efficiency, and interpretability, thoughtfully designed structured outputs will be necessary to produce a useful tool.

### 3. Retrieval-Augmented Generation (RAG) and Vector Databases

**Implementation:**
RAG of QAIAT's up-to-date vector databases would pass into our LLM process:
- Context of the interview and the speakers
- Documentation on processing Q&A interviews
- Background regarding the anticipated subject matter
- Etc.

**Justification:** This system is intended to support interviewers by supplying them with context-aware recommendations, with intention to leverage them for meaningful discussion. Context will be a crucial element of providing useful insights to the interviewers.

### 4. Evaluation Frameworks

**Evaluations will include:**
- **Human evals** - Important for validating the impact on the conversation from each stakeholder's perspective, validating user interfacing, confirming validity and professional accuracy of output, and confirming it meets real-world needs securely and efficiently
- **LLM-as-Judge** - Will support human evals and likely enhance trustworthiness if used as part of the output generation process in addition to pre-deployment and post-deployment evaluations
- **String comparison** - Used to gain confidence the output is formatted in a manner that serves niche Q&A interview purposes well, to adapt the tool with targeted user feedback

**Justification:** Various evaluations will be required to establish trust from the interviewer, interviewee, and audience that such a tool reinforces the quality of the Q&A conversation effectively and securely.

### 5. Observability Tools

**Components:**
- **Tracing** - Coordination element to time AI feedback appropriately and implement the chain of prompts with well-documented results
- **Ground Truth Datasets** - Allows for enforcement of data structures required of the system's interim and final outputs
- **Prompt Versioning** - Allows for understanding sources of variation in prompt outputs over time

**Justification:** Without use of observability tools, we cannot establish cause-effect relationships in changes that improve the performance of the tool.

### 6. Guardrails

- We will need to carefully establish a priori and experience-based guardrails on system output (e.g., treatment of expletive terms)
- Ultimately the interviewer and production will be responsible for final human-in-the-loop decisions

## Technical Approach

### High Level Development Process

1. **Audio Capture & Streaming**
2. **Audio Transcription** with speaker tagging, accurate punctuation, and structured text formatting
3. **Assign Metadata** to transcription (e.g., identify Q&A pairs and topics addressed)
4. **QAIAT Trigger** initiates LLM processing based on objective conversation markers
5. **When Trigger Detected**, Submit Transcript for LLM Processing
6. **LLM Processing** - Includes prompts, RAG, guardrails, observability functions, live LLM-as-Judge evaluations, and structured output formats
7. **Parse LLM Responses**
8. **Transform Parsed LLM Responses** into Final Format for use by Interviewer/Production

### Tools, Models, and Services

- **Audio capture** - Through local microphone tool
- **Audio streaming** - Through continuous streaming service like WebSocket
- **Audio transcription** - Through service offering low-latency and high-accuracy solutions (e.g., AssemblyAI)
- **Transcription metadata enhancement** - Through same service as audio transcription
- **Keyword or Context Trigger** - Python code that analyzes transcript output, searches for triggers, and submits chunks to LLM
- **Vector Store Database** - For context enrichment (e.g., ChromaDB)
- **LLM APIs** - For main LLM and LLM-as-Judge[s]
- **Code to Parse LLM API output**
- **Final Output to Dashboard** - Backend and frontend processes for transmitting parsed LLM API output to visual user interface

## Example Prompts & Expected Outputs

### Topic Drift Detection Feature

**Sample Prompt:**
```
TOPIC_SHIFT_EVIDENCE_DETECTION_PROMPT = Your role is to analyze this segment of an interview transcript and extract structured evidence relevant to assessing the consistency or shift in topic. For this question-response pair, provide the following information with specific citations:
- Question text with key terms that establish the topic domain
- Any explicit transition phrases or topic shift markers
- Introduction of new terms or concepts not present in the question

For each extracted element, provide:
1. The exact text with citation
2. Its position in the conversation
3. Its role in topic development
```

**Desired Output Structure (JSON):**
```json
{
  "topic_shift_analysis": {
    "conversation_sequences": [
      {
        "sequence_id": "number",
        "question": {
          "text": "string"
        },
        "response": {
          "semantic_metrics": {
            "similarity_score": "number (0.0 to 1.0)",
            "evidence": "detailed description of semantic relationship",
            "justification": "thorough analysis of score assignment"
          },
          "progression": {
            "sentences": [
              {
                "text": "string",
                "semantic_assessment": {
                  "evidence": "specific semantic relationship evidence",
                  "justification": "detailed analysis of semantic patterns"
                },
                "classification": {
                  "category": "direct_continuation | natural_progression | topic_redirection | topic_evasion | admitted_limitation",
                  "confidence": "number (0.0 to 2.0)",
                  "evidence": "string",
                  "justification": "string"
                }
              }
            ],
            "topic_changes": [
              {
                "change_point": "string",
                "semantic_distance": {
                  "category": "minor|moderate|major",
                  "measurement": "number (0.0 to 1.0)",
                  "evidence": "string"
                }
              }
            ]
          }
        }
      }
    ]
  }
}
```

## Evaluation Strategy

### Methods

#### Human Evaluation
- **User Experience**: Thumbs up/down for insights provided to the interviewer dashboard
- **Expert Evaluation**: Learn from experts their experience-based processes of breaking down interviews (pre-interview, mid-interview, and post-interview), and understand key intervention opportunities for which QAIAT would have the greatest likelihood of impact

#### LLM-as-Judge
- Deploy LLMs to assess output to validate the tool before and during its use
- Example: Use LLM judges for measuring consistency and relevance of QAIAT's judgments, or for ranking the prioritization of a recommended intervention

#### String Comparison
- Compare inputted transcript to outputs to ensure cited text matches exactly to inputs
- Validate that metadata enhancements to transcripts are accurate (e.g., names of speakers, identified topics)

### Metrics
- Rate of Acceptance of recommended AI interventions used by interview
- Latency in insight delivery
- Transcription Accuracy
- Structural Accuracy (validation of output reliability in satisfying structural requirements)
- Validity and Explainability of Recommendations (based on expert evaluations, user experience testing and surveys, LLM-as-Judge Scoring)

## Observability Plan

The observability plan relies on the following elements:

1. **Ground Truth Datasets** and targeted logging & error messaging to validate that LLM API responses throughout the chain of processing are consistent and complete. We will develop this dataset based on feedback from expert interviewers and production teams, and after validating and refining the final intervention outputs through testing with key stakeholders.

2. **Flow Tracing** - The flow of inputs and outputs should be traced at each point of transition with metrics to assess latency, cost, and data leakage, particularly for the LLM calls where LLM outputs are used as inputs for downstream LLM calls. This will be a product of system-specific code and services such as Langsmith through LangChain.

3. **Prompt Versioning and LLM Testing** - Particularly as LLMs improve and options continue to expand, prompt versioning and LLM testing will be important for ensuring a consistent quality of results is satisfied or exceeded over time.
