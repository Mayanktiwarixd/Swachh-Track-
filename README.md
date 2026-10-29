# Swach Track — sanitation reporting prototype

Three role-based views: Reporter, Staff, Supervisor. The apps share one Express API and MongoDB-backed ticket/account models. The application starts with **no seeded/demo tickets or accounts**.

## Requirements
- Node.js 18+
- MongoDB local or MongoDB Atlas for persistent storage

## Setup
1. Copy `.env.example` to `.env`.
2. Set a long random `JWT_SECRET` and a valid `MONGODB_URI`.
3. Configure `AUTHORITY_ACCOUNTS_JSON` with accounts issued by the school/authority, for example:

```env
AUTHORITY_ACCOUNTS_JSON=[{"id":"STF-001","name":"Ravi Kumar","role":"staff","password":"replace-with-a-strong-password"},{"id":"SUP-001","name":"Supervisor Name","role":"supervisor","password":"replace-with-a-strong-password"}]
```

Use unique, strong passwords. This simple environment-based account provisioning is suitable for a hackathon prototype only; production deployment should use a protected authority admin panel, hashed staff passwords, rate limiting, HTTPS, and stronger session management.

4. Install and run:

```bash
npm install
npm start
```

Open `http://localhost:3000`. Reporter users can register themselves. Staff and supervisors log in using their individual authority-issued ID and password. Each signed-in user sees their own name and a generated digital ID card. Navigation between other roles is hidden.

## Role flow
- Reporter creates a complaint and can view only their own reports.
- Supervisor reviews tickets, assigns a staff ID, adjusts priority, and verifies/reopens completed tickets.
- Staff sees tickets assigned to their individual ID/name and updates progress/evidence.
- Photos are accepted as image data URLs (up to 4 MB per photo) for this prototype.
- Supervisor charts use live ticket data; with no tickets, charts show zero/empty data rather than seeded examples.

## Data and security notes
- No demo records are seeded. In-memory fallback is empty and resets on restart; MongoDB is required for persistence.
- This is not production-ready authentication. Do not use real personal data or deploy publicly before security review.
