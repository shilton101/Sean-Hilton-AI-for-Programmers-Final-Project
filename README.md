# Sean-Hilton-AI-for-Programmers-Final-Project
README file contains Final Project Memo based on Option 2

Q&A Interview Assisting Tool (QAIAT)
If your capacity allows, please share any practical feedback on the proposal that you believe would support this idea or raise my awareness of existing solutions. 
Thank you to the Section Team for sharing your content & expertise.

Project Overview
Description of Core Idea: The current state of non-AI-assisted Question-and-Answer (Q&A) interviewing relies largely on the interviewer’s own skills and interests in managing key interview elements, including but not limited to:

Clarifying the intent of questions asked
Asking follow-up questions to dig further into the meaning of labels or nuanced content
Noting when the speaker appears to have avoided or misunderstood questions

With the consent of interviewers and interviewees, the Q&A Interview Assisting Tool is designed to actively support interview management in (near) real-time. This tool analyzes interview audio transcripts to help provide an intuitive basis for ensuring the Q&A discussion reflects a meaningful exchange and minimizes the likelihood of preventable miscommunications. 

This tool will benefit key Q&A Interview stakeholders in the following ways:

Interviewers
AI-enhanced interview format may attract interest from potential interviewees and audiences.
When used transparently and with consent (necessary conditions for licensing this product), AI support may provide interviewers with a responsive approach for handling dodged questions, proposing targeted follow-up questions, and seeking greater clarity throughout the interview, all ultimately at the interviewer’s discretion.
May relieve performance pressure to have an AI assistant as backup for safeguarding interview quality.

Interviewees
If used transparently and with consent, the tool may relieve potential concerns regarding interviewer bias.
May give interviewees more agency in the interviewing process, if interviewee is consulted on how QAIAT is used.
Through validation testing with experts and audiences, we would aim to demonstrate that using QAIAT results in more engaging and meaningful conversations.

Audience
AI-enhanced interview format may attract interest from audiences who enjoy interviews focused on deeper understanding.
Could train the QAIAT system based on audience preferences for seeking clarity and posing follow-up questions.
If used transparently, it may give audiences greater awareness of the decisions traditional interviewers implicitly make over the course of an interview, and how that impacts conversations.

Use Case & Workflow
Beneficiary Personas: 
Q&A Interviewers such as podcasters, local Q&A event hosts, certain course instructors using Q&A for pedagogical purposes, certain therapists, certain recruiters.
Limitations:
Requires consenting participants.
Requires transparent implementation.
Requires audio feed, low-latency transcription, and low latency LLM analysis.
Requires experienced interviewers with training on integrating AI insights into discussion.
Requires secure, careful handling of any sensitive subject matter, both technically and interpersonally.

AI Improvement & Automation:
Automates (and may improve) semantic detection of disconnect between interview questions and answers.
Automates development of follow-up questions using (near) real-time transcript data.
When used with transparency and consent, QAIAT improves the experience of enforcing interview parameters (e.g., ensuring interview questions were answered directly), giving interviewers the ability to use AI analysis as supportive backing for such judgments.

AI Features to Be Implemented
AI components:
Prompt engineering
Will be implemented to extract key details from transcripts. 
Prompts will be organized in terms of:
Categories (types of information including “Question Meaning“, “Response Relevance”, “Jargon”, etc.) and 
Processed in a chain first focusing on 
1). Detection/Citation of the component in question (e.g., jargon terminology), 
2). Interpretation of the component within context of the interview at that point (e.g., highest probability definitions of the jargon), and 
3). Recommendation of context-aware intervention designed to support interviewer (e.g., request confirmation that jargon meant 
Prompts must include details and examples that enable prioritization of transcript elements and must include variables that can be tailored to each specific interview (e.g., detection prompts may accept metadata and/or user inputs to indicate that scientific terms should be weighted more heavily for a certain interview, or to always exclude certain topics from analysis, or to return up to a certain number of terms based on the expected length of the interview)
Justification: Given the reliance of output on multi-layered LLM processes, the need to perform well in dynamic environments presented by structured interviews, the flexibility intended for the tool’s use across topics and interview formats, and the need to gracefully handle the anticipated lag between the real-time conversation and the near real-time AI feedback, prompt engineering will be essential for this project.

Structured outputs
Examples to at least provide few shot training of the LLM will be used, and will conform to the Categories and “Chain Layers” described in the prompt engineering section.
Structured Output from the LLMs will be standardized - perhaps as JSON output formats - and include prioritized detected elements, interpretations of such elements, and recommendations based on templates and prompts reviewed by interviewing experts. 
Justification: Because the system must be transparent to engender trust by all stakeholders, and to enhance reliability, efficiency, and interpretability, thoughtfully designed structured outputs will be necessary to produce a useful tool.

Retrieval-Augmented Generation (RAG) and vector databases
RAG of QAIAT’s up-to-date vector databases would pass into our LLM process: 
Context of the interview and the speakers
Documentation on processing Q&A interviews
Background regarding the anticipated subject matter
Etc.
Justification: This system is intended to support interviewers by supplying them with context-aware recommendations, with intention to leverage them for meaningful discussion. Context will be a crucial element of providing useful insights to the interviewers.

Evaluation frameworks
Evaluations will include:
Human evals - this will be important foremost for validating the impact on the conversation from each stakeholder’s perspective, for validating any user interfacing meant for the interviewer and producers, for confirming the validity, relevance, and professional accuracy of the output, and for confirming it meets real-world needs in a secure and efficient manner. The format of the output delivery for use by the interviewer and any production team will be important for its application and adoption.
LLM-as-Judge - this will support human evals and will likely enhance the trustworthiness of the tool if used as part of the output generation process in addition to pre-deployment and post-deployment evaluations.
String comparison - this will be used to gain confidence the output is formatted in a manner that serves a set of niche Q&A interview purposes well, to adapt the tool with targeted user feedback. 
Justification: Various evaluations will be required to establish trust from the interviewer, interviewee, and audience that such a tool reinforces the quality of the Q&A conversation effectively and securely.

Observability tools
Tracing - There will be a coordination element to time the AI feedback appropriately and to implement the chain of prompts so that the results are well documented in the content & context of the conversation, and so they are explainable and well justified. Tracing inputs and outputs of the process will enable measurement and improvement of these functions.
Ground Truth Datasets - Allows for enforcement of data structures required of the system’s interim and final outputs.
Prompt Versioning - Allows for understanding sources of variation in prompt outputs over time.
Justification: Without use of observability tools, we cannot establish cause-effect relationships in changes that improve the performance of the tool.

Guardrails
We will need to carefully establish a priori and experience-based guardrails on system output. A minor example might be on how to treat expletive terms.
Ultimately the interviewer and production will be responsible for final human-in-the-loop decisions.

Technical Approach
High Level Development
Audio Capture & Streaming
Audio Transcription with speaker tagging, accurate punctuation, and structured text formatting.
Assign Metadata to transcription (for example, identify Q&A pairs and topics addressed)
QAIAT Trigger initiates LLM processing based on objective conversation markers. For example, the interviewer may be provided a keyword to mark the end of each Q&A pair, allowing the system to use Q&A pairs as basic analytical units for providing its supportive insights. 
When Trigger Detected, Submit Transcript for LLM Processing. This process will submit the conversation transcript in units (such as Q&A pairs) to be processed by the LLM over the course of the conversation. Each unit will be cached so that as the conversation proceeds, processing of the current unit will have access to prior units of the conversation for context. 
LLM Processing. Includes prompts, RAG (using vector stores database), guardrails, observability functions, live LLM-as-Judge evaluations (as context before output is used), and structured output formats.
Parse LLM Responses. 
Transform Parsed LLM Responses into Final Format for use by Interviewer/Production.
Tools, models, services used:
Audio capture (through local microphone tool)
Audio streaming (through continuous streaming service like WebSocket) 
Audio transcription (through service that offers low-latency and high-accuracy solutions, perhaps like AssemblyAI)
Transcription metadata enhancement (through same service as audio transcription)
Keyword or Context Trigger for Initiating LLM API (Python code that analyzes the transcript output, searches for triggers, and submits chunks for to LLM for analysis and context cache)
Vector Store Database for Context Enrichment (perhaps through a service like ChromaDB)
LLM APIs for main LLM and LLM-as-Judge[s]
Code to Parse LLM API output
Final Output to Dashboard (backend and frontend processes for transmitting parsed LLM API output to the visual user interface, for communicating actionable interviewer insights)

Example Prompts & Expected Outputs
The following sample prompt and desired output are based on one feature of QAIAT that assists in detecting “topic drifts”, where the interviewee has moved off-topic. This would support the interviewer’s ability to observe deviations in subject matter and to reorient the interview back to key topics.
Sample prompt:
“TOPIC_SHIFT_EVIDENCE_DETECTION_PROMPT = Your role is to analyze this segment of an interview transcript and extract structured evidence relevant to assessing the consistency or shift in topic. For this question-response pair, provide the following information with specific citations:
Question text with key terms that establish the topic domain. 
Any explicit transition phrases or topic shift markers. 
Introduction of new terms or concepts not present in the question
For each extracted element, provide:
1. The exact text with citation
2. Its position in the conversation
3. Its role in topic development
Desired output:
Structured Output Strategy: We will use JSON to regulate the structure of LLM output, ensuring that each element is formatted appropriately to be used directly or as input to a downstream prompt or for parsing.
An example of such JSON output might be as follows (for illustrative purposes):
"topic_shift_analysis": {
    "conversation_sequences": [
        {
            "sequence_id": number,
            "question": {
                 "text": "string"
            },
                "response": {
                "semantic_metrics": {
                    "similarity_score": number,  // 0.0 to 1.0
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
                            "confidence": number,  // 0.0 to 2.0
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
                            "measurement": number,  // 0.0 to 1.0
                            "evidence": "string"
                        }

Evaluation Strategy
Methods:
Human Evaluation
User Experience
Ex: Thumbs up/down for insights provided to the interviewer dashboard
Expert Evaluation
Ex: Learn from experts their experience-based processes of breaking down interviews (pre-interview, mid-interview, and post-interview), and understand key intervention opportunities for which QAIAT would have the greatest likelihood of impact. Engineer prompts and overall process flow based on this feedback.
LLM-as-Judge
Deploy LLMs to assess output to validate the tool before and during its use.
Ex: Use LLM judges for measuring consistency and relevance of QAIAT’s judgments, or for ranking the prioritization of a recommended intervention.
String Comparison
Compare inputted transcript to outputs to ensure cited text matches exactly to inputs.
Validate that metadata enhancements to transcripts are accurate (e.g., names of speakers, identified topics…)
Metrics:
Rate of Acceptance of recommended AI interventions used by interview
Latency in insight delivery
Transcription Accuracy
Structural Accuracy (does validation show output reliably satisfies structural requirements)
Validity and Explainability of Recommendations (based on expert evaluations, user experience testing and surveys, LLM-as-Judge Scoring)

Observability Plan
The observability plan would rely on the following elements:
Ground Truth Datasets and targeted logging & error messaging to validate that LLM API responses throughout the chain of processing are consistent and reflect complete. We will develop this dataset based on feedback from expert interviewers and production teams, and after validating and refining the final intervention outputs through testing with key stakeholders.
The flow of inputs and outputs should be traced at each point of transition with metrics to assess latency, cost, and data leakage, particularly for the LLM calls where LLM outputs are used as inputs for downstream LLM calls. This will be a product of system-specific code and services such as Langsmith through LangChain.
Particularly as LLMs improve and options continue to expand, prompt versioning and LLM testing will be important for ensuring a consistent quality of results is satisfied or exceeded over time.
