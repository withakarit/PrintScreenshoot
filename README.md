random-download-server/
│
├── app.py
├── requirements.txt
├── start.sh
├── README.md
│
├── screenshots/
│   ├── img1.png
│   ├── img2.png
│   └── img3.png
│
└── .gitignore

import os
import random
import zipfile
from flask import Flask, send_file

app = Flask(__name__)

SCREENSHOT_FOLDER = "screenshots"
ZIP_NAME = "download.zip"

@app.route("/")
def home():
    return """
    <h2>Random Image Download Server</h2>
    <p>Acesse <a href="/download">/download</a> para baixar uma imagem aleatória.</p>
    """

@app.route("/download")
def download_random():

    files = os.listdir(SCREENSHOT_FOLDER)

    if not files:
        return "Nenhuma imagem encontrada."

    chosen = random.choice(files)

    zip_path = ZIP_NAME

    with zipfile.ZipFile(zip_path, "w") as zipf:
        zipf.write(os.path.join(SCREENSHOT_FOLDER, chosen), chosen)

    return send_file(zip_path, as_attachment=True)

if __name__ == "__main__":
    app.run(host="0.0.0.0", port=5000)

    flask

    #!/bin/bash

echo "Instalando dependencias..."
pip install -r requirements.txt

echo "Iniciando servidor..."
python app.py

chmod +x start.sh

__pycache__/
*.pyc
download.zip

# Random Download Server

Servidor simples em Python que gera um download de imagem aleatória.

## Funciona no

- Linux
- Termux
- VPS
- Replit

## Instalação

```bash
git clone https://github.com/withakarit/PrintScreenshoot
cd random-download-server
pip install -r requirements.txt
python app.py

http://localhost:5000/download
