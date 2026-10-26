# DOB98 Admin Panel + API

The Admin Panel and User Panel must point to this same API server/database for requests, approval status, and balances to synchronize.

## Backend setup
- Node.js 20+ and a private server; use HTTPS in production.
- Copy `server/.env.example` to `server/.env`.
- Set `JWT_SECRET` to a unique random secret of at least 32 characters.
- Set `ADMIN_EMAIL`. Generate a bcrypt hash for a strong admin password using the command in `server/README.md`; set `ADMIN_PASSWORD_HASH`.
- Set `APP_ORIGIN` to the deployed user-panel origin, `API_PUBLIC_URL` to the public API origin, and configure SMTP_HOST/SMTP_USER/SMTP_PASS/MAIL_FROM for Gmail verification.
- Run `npm install` and `npm start` inside `server`.
- Set the API base in both User Panel `app.js` and Admin Panel `js/admin.js` to `https://your-api-host/api`.

## Admin flow
Sign in using the credentials configured in `.env`. Deposit requests appear under Deposit Requests with the user's note/message and TrxID. Approving a pending deposit adds the amount to that user's ledger exactly once. Rejecting a pending withdrawal refunds its reserved amount; approving marks it processed and keeps the reservation. Admin should independently verify payment receipts with the payment provider; a TrxID/message is not proof of payment.

## Payment configuration
Set the bKash receiving number in Admin Settings. Current backend supports bKash only; Nagad/Rocket are not active in this build.

## Security / deployment notes
This is a prototype scaffold, not a certified real-money gambling platform. Six-digit numeric user passwords are weak; the format is implemented only because it was explicitly requested. Use strong admin credentials, HTTPS, SMTP, backups, payment reconciliation, audit logging, rate limiting, and a qualified security review before any real deployment. Aviator is not connected to the real wallet ledger.
