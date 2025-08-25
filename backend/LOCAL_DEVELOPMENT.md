# Local Development Setup

This document explains how to set up and run the Medusa 2.0 backend locally.

## Prerequisites

- Docker and Docker Compose
- Node.js 22.x
- npm/pnpm

## Services Setup

### 1. Start Local Services

Start PostgreSQL and Redis using Docker Compose:

```bash
docker-compose up -d
```

This will start:
- PostgreSQL on port 5432 (username: `medusa`, password: `medusa`, database: `medusa`)
- Redis on port 6379

### 2. Environment Configuration

The `.env` file is already configured for local development. Key settings:

```env
DATABASE_URL=postgresql://medusa:medusa@localhost:5432/medusa
REDIS_URL=redis://localhost:6379
```

### 3. Install Dependencies

```bash
pnpm install
```

### 4. Run Database Migrations

```bash
pnpm run build
```

### 5. Seed Database (Optional)

```bash
pnpm run seed
```

### 6. Start Development Server

```bash
pnpm run dev
```

The backend will be available at `http://localhost:9000`

## Service Management

### Check Service Status
```bash
docker-compose ps
```

### View Service Logs
```bash
docker-compose logs postgres
docker-compose logs redis
```

### Stop Services
```bash
docker-compose down
```

### Reset Database (Delete All Data)
```bash
docker-compose down -v
docker-compose up -d
```

## Troubleshooting

### Connection Issues
- Ensure Docker services are running: `docker-compose ps`
- Check if ports 5432 and 6379 are available
- Verify environment variables in `.env` file

### Database Issues
- Reset the database: `docker-compose down -v && docker-compose up -d`
- Check PostgreSQL logs: `docker-compose logs postgres`

### Port Conflicts
If you have existing PostgreSQL or Redis installations, you may need to:
1. Stop local services: `sudo service postgresql stop` / `sudo service redis-server stop`
2. Or change ports in `docker-compose.yml` and update `.env` accordingly

## Production Deployment

For Railway deployment, update the `DATABASE_URL` in your Railway environment variables to use the Railway PostgreSQL service URL format:
```
postgresql://postgres:password@postgres.railway.internal:5432/railway
```
