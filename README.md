# CPU-Friendly VQA Demo

This project is a resume-friendly first pass at a visual question answering system for CPU-only environments.

## What this build can do

- Upload an image and ask a question
- Generate a candidate answer set from the question type
- Rank answers with CLIP on CPU
- Run CLIP with ONNX Runtime for faster CPU inference
- Generate open-ended answers with BLIP on CPU
- Show multiple BLIP answer candidates in the demo UI
- Show the top answer with a confidence score in CLIP mode
- Let you override the candidate answers manually for better control

## What this build does not do yet

- It does not include attention heatmaps or region highlighting yet
- It does not ship a full ONNX pipeline for BLIP yet
- BLIP is slower than CLIP on CPU, so it is best for demos, not bulk inference
- BLIP candidates are sampled, not probability-ranked, so they are best treated as alternative suggestions

## Stack

- Streamlit
- PyTorch
- Transformers
- Optimum ONNX Runtime
- CLIP
- BLIP
- Pillow

## What to download first

1. Install Python 3.10+ if it is not already installed.
2. Install the Python packages from `requirements.txt`.
3. Run the app once so Hugging Face can download the model weights automatically.
4. Expect the first ONNX CLIP run to take longer because Optimum converts the model and caches it locally.
5. Expect the first BLIP run to take longer because the model files are downloaded and cached locally.

## Project structure

```text
CV/
├── app.py
├── model/
│   ├── __init__.py
│   ├── blip_model.py
│   └── clip_model.py
├── utils/
│   ├── __init__.py
│   ├── inference.py
│   └── preprocess.py
├── requirements.txt
└── README.md
```

## Run it

```bash
pip install -r requirements.txt
streamlit run app.py
```

## Suggested next phases

1. Add confidence visualizations and latency tracking
2. Add a small evaluation set for demo-quality validation
3. Add image region highlighting for explainability
4. Add a fully ONNX-optimized BLIP-like path if you want to go deeper on CPU inference
