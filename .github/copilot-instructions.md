# Project Guidelines

## Architecture
- This repo hosts a FastAPI app behind Azure Functions ASGI integration.
- Keep Azure Functions wrapper code in [function_app.py](function_app.py) and HTTP route handlers in [WrapperFunction/__init__.py](WrapperFunction/__init__.py).
- Keep [host.json](host.json) with an empty routePrefix so FastAPI owns URL paths directly.

## Build And Test
- Create the virtual environment in the workspace root as .venv.
- Install dependencies with:
  - Windows: .venv\\Scripts\\python -m pip install -r requirements.txt
  - macOS/Linux: .venv/bin/python -m pip install -r requirements.txt
- Run locally with VS Code Run and Debug (task label func: host start) or Azure Functions Core Tools host start.
- Local verification endpoints:
  - /sample
  - /hello/{name}
- There is no formal test suite in this repo; prefer lightweight endpoint verification after changes.

## Conventions
- Use async FastAPI route handlers unless there is a clear reason not to.
- Keep the Azure Functions glue layer minimal; implement application behavior in FastAPI modules.
- Preserve runtime alignment for Python Azure Functions settings across:
  - [requirements.txt](requirements.txt)
  - [azure.yaml](azure.yaml)
  - [infra/main.bicep](infra/main.bicep)
- Respect VS Code environment settings in [.vscode/settings.json](.vscode/settings.json), especially the .venv path.

## Deployment
- Use Azure Developer CLI for deployment workflows.
- Typical flow:
  - azd up (first-time provisioning + deploy)
  - azd deploy (code-only updates)
- For CI/CD setup, follow repository guidance in [README.md](README.md).

## Reference Docs
- Setup and usage: [README.md](README.md)
- Contribution process: [CONTRIBUTING.md](CONTRIBUTING.md)
- Infrastructure definitions: [infra/main.bicep](infra/main.bicep)
- Local run tasks: [.vscode/tasks.json](.vscode/tasks.json)