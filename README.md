## learn to composerize public app
simple blog application using express js and mongodb

# Blog App

Aplikasi blog sederhana menggunakan Node.js dengan Express, EJS, dan MongoDB.

## Prerequisites

- Docker & Docker Compose
- Node.js 11+ (untuk development lokal)

## Setup & Installation

### Dengan Docker Compose (Recommended)

1. Clone repository
```bash
git clone <repo-url>
cd blog-app
```

2. Jalankan aplikasi
```bash
docker compose up
```

Aplikasi akan accessible di `http://localhost:3000`

### Penjelasan Docker Compose

**File: `docker-compose.yml`**

```yaml
services:
  mongodb:          # Service MongoDB
    image: mongo:4.0
    ports:
      - "27017:27017"
    volumes:
      - mongodb_data:/data/db
    networks:
      - blog-network

  app:              # Service Node.js App
    build: .
    ports:
      - "3000:3000"
    environment:
      MONGODB_URI: mongodb://mongodb:27017/blogapp
    depends_on:
      - mongodb     # App menunggu MongoDB siap
    networks:
      - blog-network
```

**Penjelasan penting:**
- `MONGODB_URI: mongodb://mongodb:27017/blogapp` → `mongodb` adalah nama service (hostname dalam network)
- `depends_on: mongodb` → Memastikan MongoDB dimulai lebih dulu
- `networks: blog-network` → Kedua container terhubung dalam network yang sama

## Development Lokal (Tanpa Docker)

1. Install dependencies
```bash
npm install
```

2. Setup MongoDB
```bash
# Pastikan MongoDB running di localhost:27017
# atau ubah MONGODB_URI di app.js
```

3. Jalankan aplikasi
```bash
npm start
# atau
node app.js
```

## Troubleshooting

### Error: "connection timed out"
Pastikan:
1. Connection string menggunakan hostname yang benar:
   - Docker: `mongodb://mongodb:27017/blogapp`
   - Lokal: `mongodb://localhost:27017/blogapp`

2. Restart container:
```bash
docker compose down
docker compose up
```

### Port sudah digunakan
```bash
docker compose down
# atau kill process yang menggunakan port
```

## Project Structure

```
blog-app/
├── app.js              # Main application file
├── Dockerfile          # Docker configuration
├── docker-compose.yml  # Docker Compose configuration
├── package.json        # Node dependencies
├── routes/             # API routes
├── models/             # Database models
└── views/              # EJS templates
```

## Tech Stack

- **Runtime:** Node.js
- **Framework:** Express.js
- **Template:** EJS
- **Database:** MongoDB
- **Containerization:** Docker & Docker Compose

## License

MIT

## screenshot page
<img src="/blog.png" alt="Alt text" width="300">

<img src="/anfield.png" alt="Alt text" width="300">
