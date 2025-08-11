### 🔄 Project Awareness & Context

- **Always read `PLANNING.md`** at the start of a new conversation to understand the project's architecture, goals, style, and constraints.
- **Check `TASK.md`** before starting a new task. If the task isn’t listed, add it with a brief description and today's date.
- **Use consistent naming conventions, file structure, and architecture patterns** as described in `PLANNING.md`.
- **Use venv_linux** (the virtual environment) whenever executing Python commands, including for unit tests.

### 🧱 Code Structure & Modularity

- **Never create a file longer than 500 lines of code.** If a file approaches this limit, refactor by splitting it into modules or helper files.
- **Organize code into clearly separated modules**, grouped by feature or responsibility.

  For platform-specific solutions, refer to platform-specific documentation for solution organization best practices.

  For all custom solutions, follow a general solution organization that separates frontend code, backend code, build scripts, and configuration files into distinct directories.
  ```bash
  /
  ├── app/            # Root of all frontend and backend code for the app
  │   └── fed/        # Directory for all frontend code including static assets like images, JS, CSS, and HTML. Follow framework-specific documentation for additional best practices
  │   └── bed/        # Directory for all backend code including APIs, data access layer, processes, scripts, agents, etc.
  ├── build/          # All build-specific configuration files for containerization, CI/CD, and local development
  ├── config/         # All configuration files for higher environments that need to be source controlled. Used to streamline automated deployment of configuration changes
  ├── .gitignore      # Standard .gitignore file location in the root of the solution.
  ├── .env.example    # Example .env file with all required environment variables, descriptive comments of the intended use, and documentation for retrieving actual values
  ├── README.md       # Detailed README about the solution contents. This should act as a llms.txt for the solution. This file is required if it does not exist.
  ```

  To effectively organize by feature, maintain the distinction of frontend and backend code and don't be afraid to duplicate folders in both fed and bed directories. Here is a good example of a feature set for listing an arbitrary entity called "projects" and viewing a specific project page written in React.js and Python Fast API:
  ```bash
  /
  ├── app/
  │   ├── fed/
  │   │   └── projects/
  │   │       ├── projects-list/
  │   │       │   ├── components/
  │   │       │   │   ├── ProjectCard/
  │   │       │   │   │   ├── ProjectCard.tsx
  │   │       │   │   │   ├── ProjectCard.module.css
  │   │       │   │   │   └── index.ts
  │   │       │   │   ├── ProjectList/
  │   │       │   │   │   ├── ProjectList.tsx
  │   │       │   │   │   ├── ProjectList.module.css
  │   │       │   │   │   └── index.ts
  │   │       │   │   └── ProjectFilters/
  │   │       │   │       ├── ProjectFilters.tsx
  │   │       │   │       ├── ProjectFilters.module.css
  │   │       │   │       └── index.ts
  │   │       │   ├── hooks/
  │   │       │   │   └── useProjectsList.ts
  │   │       │   ├── services/
  │   │       │   │   └── projectsListApi.ts
  │   │       │   ├── types/
  │   │       │   │   └── projectsList.types.ts
  │   │       │   └── pages/
  │   │       │       └── ProjectsListPage.tsx
  │   │       └── project/
  │   │           ├── components/
  │   │           │   ├── ProjectDetail/
  │   │           │   │   ├── ProjectDetail.tsx
  │   │           │   │   ├── ProjectDetail.module.css
  │   │           │   │   └── index.ts
  │   │           │   ├── ProjectEdit/
  │   │           │   │   ├── ProjectEdit.tsx
  │   │           │   │   ├── ProjectEdit.module.css
  │   │           │   │   └── index.ts
  │   │           │   └── ProjectActions/
  │   │           │       ├── ProjectActions.tsx
  │   │           │       ├── ProjectActions.module.css
  │   │           │       └── index.ts
  │   │           ├── hooks/
  │   │           │   ├── useProject.ts
  │   │           │   └── useProjectMutations.ts
  │   │           ├── services/
  │   │           │   └── projectApi.ts
  │   │           ├── types/
  │   │           │   └── project.types.ts
  │   │           └── pages/
  │   │               ├── ProjectDetailPage.tsx
  │   │               └── ProjectEditPage.tsx
  │   └── bed/
  │       └── api/
  │           ├── projects/
  │           │   ├── models/
  │           │   │   └── projects_model.py
  │           │   ├── services/
  │           │   │   └── projects_service.py
  │           │   ├── schemas/
  │           │   │   └── projects_schemas.py
  │           │   └── router.py
  │           └── project/
  │               ├── models/
  │               │   └── project_model.py
  │               ├── services/
  │               │   └── project_service.py
  │               ├── schemas/
  │               │   └── project_schemas.py
  │               └── router.py
  ```

  For generative AI agentic workflow solutions, organize all agents in
  ```bash
  app/agents/
  ├── configure_observability.py
  ```
  - `agent.py` - Main agent definition and execution logic
  - `tools.py` - Tool functions used by the agent
  - `prompts.py` - System prompts
- **Use clear, consistent imports** (prefer relative imports within packages).
- **Use python_dotenv and load_env()** for environment variables.

### 🧪 Local Development
- ** Always assume local environments will be containerized using Docker.
- ** Always assume that frontend developers and backend developers are different resources with different local environments.

### 🧪 Testing & Reliability

- **Always create Pytest unit tests for new features** (functions, classes, routes, etc).
- **After updating any logic**, check whether existing unit tests need to be updated. If so, do it.
- **Tests should live in a `/tests` folder** mirroring the main app structure.
  - Include at least:
    - 1 test for expected use
    - 1 edge case
    - 1 failure case

### ✅ Task Completion

- **Mark completed tasks in `TASK.md`** immediately after finishing them.
- Add new sub-tasks or TODOs discovered during development to `TASK.md` under a “Discovered During Work” section.

### 📎 Style & Conventions

- **Use Python** as the primary language.
- **Follow PEP8**, use type hints, and format with `black`.
- **Use `pydantic` for data validation**.
- Use `FastAPI` for APIs and `SQLAlchemy` or `SQLModel` for ORM if applicable.
- Write **docstrings for every function** using the Google style:
  ```python
  def example():
      """
      Brief summary.

      Args:
          param1 (type): Description.

      Returns:
          type: Description.
      """
  ```

### 📚 Documentation & Explainability

- **Update `README.md`** when new features are added, dependencies change, or setup steps are modified.
- **Comment non-obvious code** and ensure everything is understandable to a mid-level developer.
- When writing complex logic, **add an inline `# Reason:` comment** explaining the why, not just the what.

### 🧠 AI Behavior Rules

- **Never assume missing context. Ask questions if uncertain.**
- **Never hallucinate libraries or functions** – only use known, verified Python packages.
- **Always confirm file paths and module names** exist before referencing them in code or tests.
- **Never delete or overwrite existing code** unless explicitly instructed to or if part of a task from `TASK.md`.
