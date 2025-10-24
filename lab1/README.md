# Lab 1: Simple HTTP File Server

## Purpose
Implementation of a simple HTTP server using TCP sockets, capable of serving static files (HTML, images, PDFs) and generating directory listings.

## Project Structure
```
lab1/
  client.py
  compose.yaml
  Dockerfile
  README.md
  server.py
  www/
    index.html
    europlasmet/
      2025-10-24 14.47.46.jpg
      2025-10-24 14.47.50.jpg
    reports/
      aproape_gata (1).pdf
      numar.pdf
      terminat.pdf
```

## Running Instructions

### Local (Python)
```zsh
python3 server.py www
```
Access: http://localhost:8080

### Client
```zsh
python3 client.py 127.0.0.1 8080 /index.html .
python3 client.py 127.0.0.1 8080 /europlasmet/2025-10-24\ 14.47.46.jpg .
python3 client.py 127.0.0.1 8080 /reports/numar.pdf .
```

### Docker
Build:
```zsh
docker build -t lab1-server .
```
Run:
```zsh
docker run --rm -p 8080:8080 lab1-server
```

### Docker Compose
```zsh
docker compose up --build
# To stop:
docker compose down
```

## Features
- Serves HTML, PNG, JPG, PDF files
- Automatic directory listing with links
- Path normalization for security
- Returns 404 for missing or unsupported files
- Can be started quickly with Docker or Compose

## HTTP Testing Examples
- Main directory listing:
```zsh
curl http://localhost:8080/
```
- Subdirectory listing:
```zsh
curl http://localhost:8080/reports/
```
- Headers only:
```zsh
curl -I http://localhost:8080/
```
- Download PDF/JPG:
```zsh
curl http://localhost:8080/reports/numar.pdf -o numar.pdf
curl http://localhost:8080/europlasmet/2025-10-24%2014.47.46.jpg -o photo.jpg
```

## Notes
- For live editing, uncomment the `volumes` section in `compose.yaml`.
- The server processes requests sequentially (one at a time).
- Directory and file listings are generated automatically.

## Author
Moraru Gabriel
24.10.2025
