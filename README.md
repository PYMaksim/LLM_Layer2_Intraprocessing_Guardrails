# LLM Layer 2: Intra-Processing Guardrails

This repository demonstrates **Layer 2 (Intra-processing)** security for Large Language Models. We implement a middleware "Guardrail" that intercepts and validates `tool_calls` (Function Calling) in real-time before they are executed.

## 🛡️ Goal
To prove that LLM agents should not be trusted with direct execution rights. We place a deterministic security layer between the model's decision and the API call.

## 📋 Project Flow
1.  **Tool Definition:** We define a `book_flight` function and provide its JSON Schema to the LLM.
2.  **The Attack:** We prompt DeepSeek V4 to book a flight exceeding the budget ($120,000 / Business class).
3.  **The Intercept (Guardrail):** The model generates a valid `tool_call`. Our Python code catches this JSON *before* execution.
4.  **Validation:** The Guardrail checks the `price` argument. Since $120k > $50k limit, the call is blocked.

## 📊 Key Findings
*   **LLMs are "Brains", not "Actors":** Models are great at deciding *what* to do, but they lack context for *safety*. 
*   **Middleware is Mandatory:** Without Layer 2, any successful Prompt Injection (from Layer 1) could lead to real-world financial or data loss.
*   **Determinism:** Code-based Guardrails provide guarantees that model fine-tuning cannot.

## 💻 Tech Stack
*   **API:** Yandex Cloud (DeepSeek V4 Flash)
*   **Lang:** Python (`openai` SDK)
*   **Env:** Google Colab

## 📜 License
MIT
