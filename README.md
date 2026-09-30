# TikTok & Douyin Video Downloader

A lightweight self-hosted video downloader for **TikTok** and **Douyin (抖音)**.

Paste a public video URL — or simply paste the full Douyin share text — and the application will automatically extract the video link and prepare the video for download.

Designed for users who want a simple web interface while keeping the download service under their own control.

---

## Features

- TikTok video download
- Douyin video download
- Automatic Douyin URL extraction
- Supports full Douyin share text
- TikTok short-link support
- Simple web interface
- Self-hosted backend
- Local API service
- Cloudflare Tunnel support
- Docker-based Douyin / TikTok API service
- No browser extension required
- No software installation required for website visitors

---

## Douyin Share Text Support

You do not need to manually extract the Douyin URL.

For example, you can paste the entire text copied from the Douyin app:

```text
3.89 复制打开抖音，看看【Example的作品】
这是一个抖音视频的分享文字
https://v.douyin.com/xxxxxxxx/
01/21
```

The application automatically detects:

```text
https://v.douyin.com/xxxxxxxx/
```

and sends the extracted URL to the video parser.

---

## Supported Platforms

### TikTok

Supported URL formats include:

```text
https://www.tiktok.com/@username/video/xxxxxxxx
https://vm.tiktok.com/xxxxxxxx/
https://vt.tiktok.com/xxxxxxxx/
```

### Douyin

Supported formats include:

```text
https://www.douyin.com/video/xxxxxxxx
https://v.douyin.com/xxxxxxxx/
```

You can also paste the complete share text copied directly from the Douyin app.

---

## How It Works

```text
User Browser
     │
     ▼
Web Interface
     │
     ▼
Cloudflare Worker
     │
     ▼
Cloudflare Tunnel
     │
     ▼
Local Node.js Backend
     │
     ▼
Douyin / TikTok API
     │
     ├── TikTok
     └── Douyin
     │
     ▼
Video Download
```

The public website does not need direct access to the local machine.

Cloudflare Tunnel securely connects the public frontend with the local backend.

---

## Technology Stack

- Node.js
- JavaScript / ES Modules
- Docker
- Cloudflare Workers
- Cloudflare Tunnel
- Douyin / TikTok parsing API

The Douyin and TikTok parsing service can be integrated with:

**Douyin_TikTok_Download_API**

```text
https://github.com/Evil0ctal/Douyin_TikTok_Download_API
```

---

## Project Structure

```text
tiktok-v5/
├── server.mjs
├── shared.mjs
├── publish.mjs
├── config.local.json
├── tunnel.yml
├── cloudflared
├── worker/
│   ├── index.mjs
│   └── page.mjs
└── logs/
```

The API service can run separately through Docker.

---

## Requirements

Recommended environment:

```text
Node.js 20+
Docker Desktop
Cloudflare account
Cloudflare Tunnel
```

Tested primarily on macOS.

The project can also be adapted for Linux servers.

---

## Configuration

Create your local configuration file:

```json
{
  "port": 43127,
  "token": "YOUR_PRIVATE_TOKEN",
  "douyinDtkUrl": "http://127.0.0.1:8000",
  "douyinDtkApiKey": "YOUR_API_KEY"
}
```

Do not commit your real configuration file to GitHub.

Add it to `.gitignore`:

```gitignore
config.local.json
.env
logs/
*.log
```

Never expose:

- API keys
- Cloudflare credentials
- Tunnel credentials
- Cookies
- Authentication tokens

---

## Start the Backend

```bash
cd /path/to/tiktok-v5
node server.mjs
```

The backend runs locally on:

```text
http://127.0.0.1:43127
```

A `401 Unauthorized` response from the root endpoint can be normal because the backend requires authentication.

---

## Start the API Service

The TikTok / Douyin parsing API can be deployed through Docker.

```bash
docker compose up -d
```

The local API service can run on:

```text
http://127.0.0.1:8000
```

Health check:

```bash
curl http://127.0.0.1:8000/healthz
```

---

## Start Cloudflare Tunnel

```bash
./cloudflared tunnel --config tunnel.yml run
```

Cloudflare Tunnel allows the public Worker to communicate with the backend without exposing the local machine directly to the Internet.

---

## Usage

### Step 1

Copy a TikTok or Douyin video link.

For Douyin, you can also copy the complete share text.

### Step 2

Paste it into the input field.

### Step 3

Click:

```text
获取视频
```

### Step 4

When the video is ready, click:

```text
下载 MP4
```

---

## Why This Project?

Many online video download websites rely on third-party services that may contain advertisements, redirect users, track visitors, disappear without notice, or limit download frequency.

This project provides a self-hosted alternative.

You control:

```text
Frontend
Backend
API
Domain
Cloudflare Tunnel
Download workflow
```

It can be used as a private downloader or deployed as a small public web service.

---

## Security

This project separates the public website from the local backend.

```text
Browser
   ↓
Cloudflare
   ↓
Authenticated backend
   ↓
Local API
```

Sensitive API keys should only exist on the backend.

Never place API keys directly inside frontend JavaScript.

---

## Roadmap

- Faster TikTok parsing
- Faster Douyin parsing
- Direct media streaming
- Download progress display
- Better mobile support
- Video metadata preview
- Thumbnail preview
- Automatic filename generation
- Docker one-click deployment
- Linux deployment support

---

## Disclaimer

This project is intended for downloading **publicly accessible videos** for personal, educational, archival, or other lawful purposes.

Users are responsible for complying with applicable laws, copyright regulations, TikTok terms of service, Douyin terms of service, and the rights of content creators.

Do not use this project to download, distribute, or republish content without permission where permission is required.

This project is not affiliated with, endorsed by, or sponsored by TikTok, ByteDance, or Douyin.

---

## Acknowledgements

Thanks to the open-source community and the contributors behind **Douyin_TikTok_Download_API** for providing the API infrastructure used for TikTok and Douyin parsing.

---

## Support

If you encounter a problem, please open a GitHub Issue.

When reporting an issue, please include:

```text
Operating System
Node.js version
Docker version
Video platform
Example URL type
Error message
```

Do not include your API keys, cookies, tokens, or other private credentials.

---

## Star the Project

If this project is useful to you, consider giving it a ⭐ on GitHub.

Your support helps the project reach more users and encourages continued development.

---

## 中文说明

这是一个可以自行部署的 **TikTok + 抖音视频下载工具**。

主要功能：

- 支持 TikTok 视频链接
- 支持抖音视频链接
- 支持 TikTok 短链接
- 支持抖音短链接
- 支持直接粘贴完整抖音分享文案
- 自动从抖音分享文字中提取视频链接
- Web 网页操作
- 本地 API
- Docker 部署
- Cloudflare Tunnel
- 可作为私人下载工具使用

抖音用户可以直接复制：

```text
复制打开抖音……
https://v.douyin.com/xxxxxxx/
```

整段粘贴到网站，无需手动删除其他文字。

系统会自动识别其中的视频链接。

---

## Suggested GitHub Repository Name

```text
tiktok-douyin-video-downloader
```

Alternative:

```text
TikTok-Douyin-Video-Downloader
```

## Suggested GitHub Description

```text
Self-hosted TikTok & Douyin video downloader with automatic Douyin share-text URL extraction, Docker API and Cloudflare Tunnel support.
```

## Suggested GitHub Topics

```text
tiktok
douyin
tiktok-downloader
douyin-downloader
video-downloader
tiktok-video-downloader
douyin-video-downloader
nodejs
docker
cloudflare
cloudflare-workers
self-hosted
```
