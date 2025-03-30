# WeChat OCR API Docker

[![Platform](https://img.shields.io/badge/platform-linux%2Famd64%20%7C%20linux%2Farm64-blue)](https://github.com/yuchanns/wxocr)
[![Python](https://img.shields.io/badge/python-3.9-blue.svg)](https://www.python.org/downloads/release/python-390/)
[![Image](https://ghcr-badge.yuchanns.xyz/yuchanns/wxocr/tags?ignore=latest)](https://github.com/yuchanns/wxocr/pkgs/container/wxocr)
![Size](https://ghcr-badge.yuchanns.xyz/yuchanns/wxocr/size)

A containerized WeChat OCR API service with multi-architecture support (x86_64 and ARM64). This project is forked from [hx71105417/wxocr](https://github.com/hx71105417/wxocr) with additional improvements for modern environments.

<details>
<summary>WebUI Example</summary>
<img src="https://github.com/user-attachments/assets/594dd312-a65b-4c91-a562-3e148b3af4bd" alt="WebUI Example"
width="600"/>
</details>

## 🚀 Features

- Multi-architecture support (AMD64 and ARM64)
- Python 3.9 compatibility
- Docker container ready
- Simple REST API interface
- Easy deployment
- Simple web UI for testing

## 📋 Prerequisites

- Docker installed
- Git && LFS (for cloning the repository)
- Internet connection for pulling Docker images

## Quick Start

```bash
pdm run start ## build and run the container locally
```

## 🛠️ Installation

1. **Clone the Repository**
   ```bash
   git clone https://github.com/yuchanns/wxocr
   cd wxocr
   git submodule update --init --recursive
   ```

2. **Build the Docker Image**
   ```bash
   # Enable multi-architecture support (required for ARM64 hosts)
   docker run --privileged --rm tonistiigi/binfmt --install all

   # Create and use multi-architecture builder
   docker buildx create --name multiarch --driver docker-container --use

   # Build and push the image (replace the tag as needed)
   docker buildx build --platform linux/amd64,linux/arm64 \
     -t ghcr.io/yuchanns/wxocr:duo-3.9 --push .
   ```

## 🚀 Usage

1. **Start the Container**
   ```bash
   docker run -d -p 5000:5000 ghcr.io/yuchanns/wxocr:duo-3.9
   ```

2. **Test the API**
   ```bash
   # Create a test request with a base64 encoded image
   echo '{"image": "'$(base64 test_image.jpg)'"}' > data.json

   # Send the request
   curl -X POST \
     -H "Content-Type: application/json" \
     -d @data.json \
     http://localhost:5000/ocr

    # Create a test request with a URL
    echo '{"url": "https://example.com/test_image.jpg"}' > data.json

    # Send the request
    curl -X POST \
      -H "Content-Type: application/json" \
      -d @data.json \
      http://localhost:5000/ocr
   ```

## 🙏 Credits

This project builds upon the work of these excellent repositories:
- [wechat-ocr](https://github.com/swigger/wechat-ocr)
- [wxocr](https://github.com/hx71105417/wxocr)

## ⚠️ Legal Notice

**Disclaimer:** This project is intended for educational and research purposes only. Commercial use is not recommended. Users assume full responsibility for any consequences arising from their use of this software.

**Copyright Notice:** This repository serves as a container for existing open-source projects. If you believe this repository infringes upon your intellectual property rights, please contact the repository owner immediately for prompt removal. We are committed to respecting intellectual property rights and will address any concerns expeditiously.

## 📄 License

This project is open-source software licensed under the MIT license.
