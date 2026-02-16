# Local Development Guide

## Running Decap CMS Locally

### Prerequisites
- Node.js installed (check with `node --version`)

### Step 1: Enable Local Backend

Edit `admin/config.yml` and uncomment the local_backend line:

```yaml
backend:
  name: git-gateway
  branch: master

# Uncomment this line for local development:
local_backend: true
```

### Step 2: Start the Decap Server (Terminal 1)

Open a terminal and run:

```bash
npx decap-server
```

This starts the backend proxy server on port 8081. Keep this running.

### Step 3: Start a Local Web Server (Terminal 2)

Open a second terminal and run one of these options:

**Option A: Using Python (if installed)**
```bash
# Python 3
python -m http.server 8080

# Python 2
python -m SimpleHTTPServer 8080
```

**Option B: Using Node.js (npx)**
```bash
npx http-server -p 8080
```

**Option C: Using PHP (if installed)**
```bash
php -S localhost:8080
```

### Step 4: Access the CMS

Open your browser and go to:
- **Website**: http://localhost:8080/
- **CMS Admin**: http://localhost:8080/admin/

You can now edit content locally! Changes will be committed to your local Git repository.

## Quick Start Commands

```bash
# Terminal 1 - Start Decap backend
npx decap-server

# Terminal 2 - Start web server (choose one)
npx http-server -p 8080
# OR
python -m http.server 8080
```

Then visit: http://localhost:8080/admin/

## Before Deploying

Remember to comment out `local_backend: true` in `admin/config.yml` before pushing to production!

## Troubleshooting

### Port already in use
If port 8080 or 8081 is taken, use different ports:
```bash
npx decap-server --port 8082
npx http-server -p 9000
```

### Can't access /admin/
- Make sure the web server is running from the project root directory
- Check that both servers are running
- Try clearing browser cache

### Changes not saving
- Verify `decap-server` is running
- Check that `local_backend: true` is uncommented
- Ensure you're in a Git repository
