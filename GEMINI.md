# NordVPN WireGuard Config Generator

## Project Overview
This project provides tools to generate optimized WireGuard configurations for NordVPN accounts. It aims to solve the problem of manual configuration by automating server selection (based on load and proximity) and key generation.

The repository is a monorepo containing multiple implementations:
1.  **Python CLI (`nordgen/`)**: A robust command-line tool for personal use or scripting.
2.  **Web Version V2**: A full-stack web application consisting of:
    *   **Backend (`web-version-V2/web-version-V2-Backend/`)**: A high-performance Go API.
    *   **Frontend (`web-version-V2/web-version-V2-Frontend/`)**: A modern Vue.js user interface.

## Components & Usage

### 1. Python CLI (`nordgen/`)
Located in `nordgen/`, this is the primary CLI tool.

*   **Language:** Python 3.9+
*   **Dependencies:** Managed via `setuptools` (standard `pyproject.toml`). Key deps: `aiohttp`, `rich`.
*   **Entry Point:** `src/nord_config_generator/main.py` -> `cli_entry_point`

**Development Commands:**
To work on the Python CLI, navigate to `nordgen/`.
```bash
# Install in editable mode
pip install -e .

# Run the tool
nordgen

# Run key retrieval only
nordgen get-key
```

### 2. Web Backend (`web-version-V2/web-version-V2-Backend/`)
A Go service using the Fiber framework. It handles NordVPN API proxying and configuration generation.

*   **Language:** Go 1.25+
*   **Framework:** Fiber
*   **Key Files:**
    *   `main.go`: Entry point.
    *   `internal/store/`: In-memory cache for server data.
    *   `internal/wg/`: WireGuard logic.

**Commands:**
Navigate to `web-version-V2/web-version-V2-Backend/`.
```bash
# Install dependencies
go mod download

# Run in development mode (port 3000)
go run main.go

# Build for production (stripped binary)
CGO_ENABLED=0 GOOS=linux go build -ldflags="-s -w" -trimpath -o server main.go
```

### 3. Web Frontend (`web-version-V2/web-version-V2-Frontend/`)
A Vue 3 application built with Vite and Tailwind CSS.

*   **Language:** JavaScript / Vue
*   **Build Tool:** Vite
*   **Styling:** Tailwind CSS

**Commands:**
Navigate to `web-version-V2/web-version-V2-Frontend/`.
```bash
# Install dependencies
npm install

# Start development server
npm run dev

# Build for production
npm run build
```

## Conventions
*   **Code Style:**
    *   **Python:** Follows PEP 8. Uses `rich` for CLI output.
    *   **Go:** Standard Go formatting (`gofmt`). Minimalist structure.
    *   **Vue:** Composition API is preferred (`<script setup>`).
*   **Testing:**
    *   Currently, no explicit test suites were observed in the root of the sub-projects. Ensure to verify changes manually or add tests if implementing significant logic.
*   **Docker:** The project includes a `Dockerfile` in the root for containerized execution of the Python CLI.

## Key Configuration Files
*   `nordgen/pyproject.toml`: Python package metadata.
*   `web-version-V2/web-version-V2-Backend/API.md`: API documentation for the backend.
*   `web-version-V2/web-version-V2-Frontend/vite.config.js`: Frontend build configuration.
