# AI-Powered WhatsApp Message Assistant (n8n Workflow)

An enterprise-grade, multi-modal AI customer support automation built on **n8n**. This workflow acts as an autonomous WhatsApp assistant that seamlessly processes **Text, Voice Notes, and Images**, checks internal knowledge spaces using vector search, tracks historical conversational context, and responds back using matching media formats.

![Workflow Canvas](assets/Ai%20Power%20Msg%20Assistant%20.jpeg)

## 🚀 Key Architectural Pillars

The system is decoupled into four highly optimized logical stages:

1. **Ingress & Multi-Modal Routing:** Uses an initial gateway webhook connected to the **Whapi.cloud** API alongside a conditional switch block to automatically classify incoming payload structures based on message content types.
2. **Context Conversion & Extraction (LangChain Layer):** 
   * **Voice Payloads:** Streams incoming binary data directly into an OpenAI Whisper model to transcribe voice notes.
   * **Image Payloads:** Dispatches multi-part file buffers to a vision model (`gpt-4o-mini`) for prompt-driven content analysis.
3. **Retrieval-Augmented Generation (RAG) & Agentic Reasoning:** Anchored by an advanced LangChain Agent node leveraging `gpt-4.1-mini`. The agent interfaces with a Supabase Vector Store to execute semantic embedding searches alongside a Window Memory Buffer to maintain session continuity.
4. **Egress Format Matching:** Evaluates the initial structural footprint of the user interaction. If the contact initiated contact via audio, the system passes text completions to an OpenAI Audio Generation model to stream matching voice notes back through the messaging gateway.

---

## 🔧 Component Dependencies

To run or replicate this integration pipeline, you will require active accounts and authorization keys for the following services:

* **n8n Instance:** Self-hosted docker engine or cloud workspace environment.
* **Whapi.cloud Profile:** An active API key tied to an authenticated WhatsApp device instance.
* **OpenAI Developer Platform:** Access tokens supporting chat completions, vision pipelines, transcriptions, and audio synthesis.
* **Supabase Workspace:** A hosting cluster running a pre-configured vector table space.

---

## 💻 Installation & Orchestration Steps

1. Create a blank workflow template canvas in your n8n workspace panel.
2. Click the menu option in the top right, choose **Import from File**, and upload the `AI-Powered message Assistant (1).json` file from this repository.
3. Update individual HTTP Request node blocks with your private Whapi `Authorization` tokens.
4. Bind your OpenAI and Supabase credentials to their designated LangChain utility blocks inside the workflow layout.
5. Copy the live production Webhook generation address from your n8n configuration panel and register it within your Whapi configuration console to start receiving real-time payloads.
