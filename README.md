AI Joke Generator with Video Delivery

- A fully working multimodal AI pipeline that:

- Fine-tunes a small language model (Phi-1.5) on CPU

- Generates short, topical jokes

- Delivers them via CrewAI agent orchestration

- Produces video performances using HeyGen avatars
  

Key Components & Steps

- Model: Used microsoft/phi-1_5 (causal language model) from Hugging Face, fine-tuned with PEFT + LoRA

- Fine-tuning: Created a tiny JSONL dataset of joke topics + outputs, formatted with OpenAI-style chat prompts

- Training: Used transformers, datasets, trl.SFTTrainer, and peft to fine-tune on CPU (with small dataset)

- Model Wrapping: Configured with get_peft_model and LoRA adapters to reduce memory usage

- Agent Orchestration: Integrated with CrewAI to define an AI stand-up comedian agent ("Chuckles") and joke generation task

- Tool Creation: Registered the fine-tuned model as a tool using @tool decorator from crewai_tools

- Crew Execution: CrewAI routed joke prompts through the fine-tuned model via the tool

- HeyGen Integration: Used HeyGen API (/video/generate and /video_status.get) to convert jokes to avatar-delivered videos

- Fixes: Handled string serialization issues by explicitly converting CrewAI outputs to plain text before sending to HeyGen

- Testing: Verified the full flow end-to-end — topic ➝ joke ➝ avatar video — all running on CPU in Google Colab


Libraries Used
transformers, datasets, peft, trl — for model loading and fine-tuning

CrewAI, crewai_tools — for agent orchestration and tool integration

HeyGen API — for avatar-based video generation

requests, json, os, time — for API calls and data handling

Optional: gradio for UI (next step)
