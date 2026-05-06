# CNC Quote Platform 🏭

Manufacturing quote generation and DFM analysis platform with real-time pricing, CAD processing, and order management.

## Quick Start

```bash
git clone https://github.com/Aakash-Sleur/FFP.git
cd FFP
pnpm install
cp .env.example .env
pnpm dev
```

**Services:** Web (http://localhost:3000) • API (http://localhost:5001) • CAD (http://localhost:10001)

---

## 📥 Test CAD Upload

Download and test the CAD file upload functionality:

| File | Download |
|------|----------|
| **Test File 1** | [📥 Download](https://jugvsxsxfv.ufs.sh/f/ge9ipdjHrCskRKHxgFdjK1HB3SX7NWwsAnkU8aTg2I59QZ4G) |
| **Test File 2** | [📥 Download](https://jugvsxsxfv.ufs.sh/f/ge9ipdjHrCskzGm0n6Fa1IJWSRm8EC3OZdelvt7ibwGL90Y6) |


---

## Tech Stack

| Layer | Technology |
|-------|-----------|
| **Frontend** | Next.js 15, React 18, TypeScript, Tailwind CSS |
| **Backend** | NestJS, Prisma, PostgreSQL, Supabase |
| **CAD Service** | Python, FastAPI |
| **Workflows** | Go, Gin, Temporal |
| **DevOps** | Docker, pnpm workspaces, Turborepo |

---

## Architecture

```
Frontend (Next.js) ↔ API (NestJS) ↔ CAD Service (FastAPI)
              ↓
PostgreSQL + Redis
              ↑
   Workflow Service (Go/Temporal)
```

---

## Installation

### Prerequisites
- Node.js 18+, pnpm 10+
- Python 3.9+
- Docker & Docker Compose
- PostgreSQL or Supabase

### Setup
```bash
pnpm install                          # Install all workspaces
cp .env.example .env                  # Configure environment
pnpm dev                              # Start all services
# OR
docker-compose up --build             # Start with Docker
```

### Environment Files
- `apps/web/.env.local` - Frontend config
- `apps/api/.env` - Backend config
- `apps/cad-service/.env` - CAD service config

---

## Project Structure

```
FFP/
├── apps/
│   ├── web/               # Next.js frontend
│   ├── api/               # NestJS backend
│   ├── cad-service/       # Python CAD processor
│   └── workflow-service/  # Go/Temporal workflows
├── packages/shared/       # Shared types & utilities
├── docker-compose.yml
└── pnpm-workspace.yaml
```

---

## Core Features

- **Quote Generation:** Real-time pricing with geometry analysis
- **DFM Analysis:** Automated manufacturability feedback
- **File Upload:** STEP, STL, IGES, OBJ support
- **Order Management:** Status tracking and lifecycle
- **Multi-tenant:** Role-based access control
- **Payment:** PayPal integration

---

## Development

```bash
pnpm build                           # Build all
pnpm dev                             # Dev mode
pnpm test                            # Run tests
pnpm lint                            # Lint code
pnpm format                          # Format code
pnpm --filter @cnc-quote/web dev    # Web only
pnpm --filter @cnc-quote/api dev    # API only
```

---

## API Endpoints

### Auth
```
POST   /auth/login
POST   /auth/register
POST   /auth/refresh
```

### Uploads & Analysis
```
POST   /uploads                      # Upload CAD file
GET    /uploads/:id                  # Check status
POST   /dfm/analyze                  # DFM analysis
```

### Quotes & Orders
```
GET    /quotes
POST   /quotes
POST   /quotes/preview-multipart     # Preview pricing
GET    /orders
POST   /orders
PATCH  /orders/:id                   # Update order
```

---

## Configuration

### Web (`apps/web/.env.local`)
```env
NEXT_PUBLIC_API_URL=http://localhost:5001
NEXT_PUBLIC_SUPABASE_URL=your-url
NEXT_PUBLIC_SUPABASE_ANON_KEY=your-key
NEXT_PUBLIC_PAYPAL_CLIENT_ID=your-id
```

### API (`apps/api/.env`)
```env
DATABASE_URL=postgresql://user:pass@localhost:5432/db
JWT_SECRET=your-secret
SUPABASE_SERVICE_KEY=your-key
SUPABASE_STORAGE_BUCKET=cad-files
REDIS_URL=redis://localhost:6379
CAD_SERVICE_URL=http://localhost:10001
PAYPAL_CLIENT_ID=your-id
PAYPAL_CLIENT_SECRET=your-secret
```

### CAD Service (`apps/cad-service/.env`)
```env
API_PORT=10001
MAX_FILE_SIZE=100MB
TEMP_DIR=/tmp/cad-uploads
PROCESSING_TIMEOUT=300
```

---

## Docker

```bash
docker-compose up --build          # Start all services
docker-compose logs -f web         # View logs
docker-compose down                # Stop services
```

**Services:**
- api - NestJS backend
- cad-service - Python CAD processor
- web - Next.js frontend
- postgres - Database
- redis - Cache & queue
- nginx - Reverse proxy

---

## Order Lifecycle

```
NEW → PAID → IN_PRODUCTION → QC → SHIPPED → COMPLETE
```

Status transitions enforced server-side. `COMPLETE` and `CANCELLED` are terminal states.

---

## Security

- JWT-based authentication
- Role-based access control (RBAC)
- Input validation with Zod
- Prisma ORM (SQL injection prevention)
- HTTPS/SSL for all traffic
- Supabase Row-Level Security (RLS)

---

## Testing

```bash
pnpm test                 # Run all tests
pnpm test:e2e            # Playwright E2E
pnpm qa                  # QA checks
```

**Test files:**
- Unit & integration: `apps/**/*.test.ts`
- E2E: `apps/web/e2e/`
- QA: `scripts/qa-runner.js`

---

## Deployment

```bash
docker-compose build
docker-compose up -d
```

**Setup:**
1. Configure Supabase database
2. Set PayPal credentials
3. Configure email service
4. Deploy via Docker or Render

---

## Troubleshooting

**CAD Service Issues:**
```bash
docker-compose logs cad-service
curl http://localhost:10001/health
```

**Database Issues:**
```bash
grep DATABASE_URL apps/api/.env
cd apps/api && pnpm prisma db push
```

**Port Conflicts:**
Check and modify port in `docker-compose.yml` or `.env`

---

## Contributing

1. Fork repository
2. Create feature branch
3. Make changes & run tests
4. Commit with conventional messages
5. Open Pull Request

---

## License

MIT License - See [LICENSE](LICENSE) file for details

---

**Happy Manufacturing! 🏭**
