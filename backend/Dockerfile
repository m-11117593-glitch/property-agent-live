FROM python:3.11-slim

WORKDIR /app

# system deps (safe for Playwright Chromium)
RUN apt-get update && apt-get install -y \
    wget curl \
    libglib2.0-0 libnss3 \
    libx11-xcb1 libxcomposite1 libxcursor1 \
    libxdamage1 libxi6 libxtst6 \
    libatk1.0-0 libgtk-3-0 libasound2 \
    libgbm1 libxrandr2 libpangocairo-1.0-0 \
    libpango-1.0-0 libcairo2 \
    fonts-liberation \
    && rm -rf /var/lib/apt/lists/*

COPY requirements.txt .

RUN pip install --no-cache-dir -r requirements.txt

# install playwright browsers (correct way)
RUN playwright install chromium

COPY . .

EXPOSE 8000

CMD ["uvicorn", "backend.main:app", "--host", "0.0.0.0", "--port", "8000"]