# AGENTS.md

## Project Overview
- Multi-round implementation (round1=minimal, round2=full)
- Active work should be in `round2/` directory
- Uses Express with HTTP Basic Auth (`admin:admin123`)
- Base64 auth header: `YWRtaW46YWRtaW4xMjM=`

## Entrypoint
```bash
cd round2
npm start
```

## Key Runtime Facts
- Server runs on `http://localhost:3000`
- Both `/submit-settings` (POST) and `/settings-data` (GET) require auth
- Data persistence: `data/settings.json` in round2/
- Use `round2/package.json` for dependency versions

## Authentication Fix
⚠️ **Critical issue fixed**: `round2/public/index.html` now includes auth headers for both API calls using `getAuthHeaders()` helper function

## Package Structure
- `round2/` contains the production implementation
- `round1/` is a reference minimal version
- Dependencies: Express with comprehensive middleware stack

## Commands
- `npm start` - Starts the Express server
- `npm test` - Available but only shows error (no tests implemented)

## Security
- HTTP Basic Auth with hardcoded credentials (`admin:admin123`)
- Credentials in base64: `YWRtaW46YWRtaW4xMjM=`
- In production, use environment variables instead of hardcoded credentials
- Commits must follow https://www.conventionalcommits.org/en/v1.0.0/ format

## Files Created/Fixed
- `round2/public/index.html` - Added authentication headers to API calls
- `round2/package.json` - Dependencies management
- `round2/server.js` - Express server with validation and persistence
- `data/settings.json` - Stores submitted form data

## Common Pitfalls
⚠️ **Absolute must**: Requesting `/submit-settings` or `/settings-data` without auth headers returns 401
⚠️ **Critical**: Use `cd round2/` - the main code is there, not in root
⚠️ **Security**: Never commit hardcoded credentials in real deployment
⚠️ **Validation**: Form requires all fields: adminName, adminEmail, companyName, companyAddress

## Data Validation
- Email format validation
- Max length: adminName(50), adminEmail(100), phoneNumber(20), companyName(100), companyAddress(500)
- Server saves data to JSON file for persistence across restarts

## Testing
- No unit tests implemented yet
- Manual testing recommended
- Form has client-side validation with real-time feedback
- Server handles validation errors with descriptive messages

## Architecture Notes
- `server.js`: Express server with validation middleware
- `index.html`: Complete UI with Tailwind CSS, form validation, and dashboard
- `data/settings.json`: JSON file storage for form submissions
- Uses standard Express patterns with Node.js/Express
