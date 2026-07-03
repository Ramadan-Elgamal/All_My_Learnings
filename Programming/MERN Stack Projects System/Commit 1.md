## Commit 1 : "feat: initialize project structure with React client and Express server scaffolding"


### Step 1: Init the vite app for the frontend:
Run this command to scaffold your React frontend, naming the folder `client`:

```bash
npm create vite@latest client -- --template react
```

Once the scaffolding is complete, just navigate into the new folder and install the base dependencies:

```bash
cd client
npm install
```

### Step 1: Create the folder structure:
#### Run the followintg command 
#### If you are on Linux
```bash
mkdir -p src/{assets,components/{ui,form},features/{auth/{api,components,hooks,types},hooks,layouts,pages,routes,services,store,types,utils}}
```

#### If you are on Windows
##### Option 1: Use Git Bash (Recommended)
##### Option 2: The Native PowerShell Version
If you prefer to use standard Windows **PowerShell**, you have to use PowerShell syntax. Here is the exact equivalent command that achieves the same result in one go:
```powershell
$paths = @(
    "src/assets", "src/components/ui", "src/components/form",
    "src/features/auth/api", "src/features/auth/components", "src/features/auth/hooks", "src/features/auth/types",
    "src/hooks", "src/layouts", "src/pages", "src/routes", "src/services", "src/store", "src/types", "src/utils"
); foreach ($path in $paths) { New-Item -ItemType Directory -Force -Path $path }
```

### Step 2: Initialize and Install Dependencies for the backend
Run the following commands to init the app
```bash
mkdir server
cd server
npm init -y

# Core MERN dependencies
npm install express mongoose cors dotenv helmet

# Developer dependencies (Nodemon replaces ts-node-dev)
npm install -D nodemon
```

Run these Commands to Create the Structure
**For Mac, Linux, WSL, or Git Bash:**
```bash
mkdir -p src/{config,controllers,middlewares,models,routes,services,utils}
touch src/{app.js,server.js} .env .gitignore
```

**For Windows PowerShell**
```powershell
$paths = @(
    "src/config", "src/controllers", "src/middlewares", "src/models",
    "src/routes", "src/services", "src/utils"
); foreach ($path in $paths) { New-Item -ItemType Directory -Force -Path $path }
New-Item -ItemType File -Force -Path "src/app.js", "src/server.js", ".env", ".gitignore"
```

### Step 3: Add the .gitkeep files

#### Run this single command from your frontend folder once and then server folder once:
##### If you are on Linux
```bash
find src -type d -empty -exec touch {}/.gitkeep \;
```

##### if you are on Windows
```powershell
Get-ChildItem -Path src -Recurse -Directory | Where-Object { (-not $_.EnumerateFileSystemInfos().Any()) } | ForEach-Object { New-Item -Path $_.FullName -Name ".gitkeep" -ItemType "file" }
```
