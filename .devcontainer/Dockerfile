FROM python:3.10-slim

# Install system dependencies
RUN apt-get update && apt-get install -y \
    git \
    curl \
    build-essential \
    && rm -rf /var/lib/apt/lists/* \
    && apt-get clean

# Set working directory
WORKDIR /workspace/flashrag

# Copy requirements first for better caching
COPY requirements.txt .

# Install CPU-only PyTorch and dependencies to save space
RUN pip install --upgrade pip \
    && pip install --no-cache-dir torch torchvision torchaudio --index-url https://download.pytorch.org/whl/cpu \
    && pip install --no-cache-dir transformers datasets numpy PyYAML tqdm tiktoken requests nltk \
    && pip install --no-cache-dir faiss-cpu \
    && pip cache purge

# Copy source code
COPY . .

# Default command
CMD [ "bash" ]
