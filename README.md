# Records Database API

## Overview
Production-ready Express.js API for managing records records with complete validation, file uploads, and PostgreSQL support.

## Features
- ✅ Full CRUD operations with validation
- ✅ File upload support with size/type restrictions
- ✅ Email, URL, and phone number validation
- ✅ Transaction support with rollback
- ✅ Comprehensive error handling
- ✅ Health checks
- ✅ Schema introspection
- ✅ Docker and Render.com deployment ready

## Database Schema

### Table: `records`

| Field | Type | Required | Unique | Description |
|-------|------|----------|--------|-------------|
| id | BIGINT | ✅ | ✅ | Auto-generated primary key |
| name | Text(50) | ✅ | ❌ | Short text field (max 50 characters) |
| roll | Number(4) | ✅ | ✅ | Whole number (max 10 digits) |
| phone | Number(10) | ✅ | ❌ | Whole number (max 10 digits) |
| amount | Decimal(10,2) | ✅ | ❌ | Decimal number (10 total digits, 2 decimal places) |
| photo | Photo | ❌ | ❌ | Image upload field (JPG, PNG, GIF) |
| created_at | TIMESTAMP | ✅ | ❌ | Automatic timestamp |

## API Endpoints

### POST /api/save
Save a new record with validation.

**Request:**
```json
{
  "name": "value",
  "roll": "value",
  "phone": "value",
  "amount": "value"
}
```

**File Upload:** Use multipart/form-data for file fields: photo

**Response:**
```json
{
  "success": true,
  "id": 1,
  "created_at": "2024-01-01T00:00:00.000Z",
  "message": "Record saved successfully",
  "table": "records"
}
```

### GET /schema
Get current schema information.

### GET /health
Health check endpoint.

## Setup

### 1. Clone and Install
```bash
git clone <repository-url>
cd records-api
npm install
```

### 2. Configure Environment
```bash
cp .env.example .env
# Edit .env with your database credentials
```

### 3. Database Setup
```bash
# Using Docker Compose (recommended)
docker-compose up -d

# Or manually create database
createdb records
```

### 4. Start Server
```bash
# Development
npm run dev

# Production
npm start
```

## Deployment

### Docker
```bash
# Build and run
docker-compose up --build -d

# View logs
docker-compose logs -f

# Stop services
docker-compose down
```

### Render.com
1. Push code to GitHub
2. Connect repository to Render
3. Deploy automatically

## Validation Rules
- Required fields: 4 fields
- Unique constraints: 1 fields
- File uploads: 1 fields with size/type restrictions
- Email/URL/Phone: Automatic format validation
- Numeric limits: Precision and range validation

## Error Handling
All errors return structured responses:
```json
{
  "error": "Descriptive message",
  "code": "ERROR_CODE",
  "field": "field_name"  // if applicable
}
```

## Security Features
- File size limits to prevent DoS
- File type restrictions
- SQL injection protection via parameterized queries
- Input validation and sanitization
- Environment variable configuration

## Monitoring
- Health endpoint: `GET /health`
- Structured logging
- Database connection pooling
- Automatic reconnection

## License
MIT License - See LICENSE file for details

## Support
For issues and feature requests, please use the GitHub issue tracker.