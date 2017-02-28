# Specification file
(back to [vision](README.md))

### Format:
 - YAML format (simple, low-overhead, easily read by python)

Issues:
 - DRY (wish to avoid copy and pasting)

Project-level specifications:
 - authentication model

Options for resource specification:
 1. URL-based spec (endpoint-by-endpoint)
 2. resource-based spec (model-by-model)
 3. frontend-based spec (given this is a full-stack generator, specify the pages in the angular app, and work backward to endpoints)
 4. actions-based spec (user stories -> front-end pages -> REST API)

**What would this look like for a simple app?**
Toy app:
Project management app.
Users log in with google OAuth
Two categories of user: project managers and contributors
Projects belong to one or more project managers
Tasks belong to projects
Subtasks belong to tasks
Tasks/subtasks have a short and long description, start date, due date, and progress updates
Tasks/subtasks are assigned to contributors/project managers
Each user has a to-do list page, calendar page, and the ability to update their tasks.
Project managers have a global view of their projects, view per project, and the ability to create/assign tasks/subtasks to contributors.

## Option 1 (URL-based spec):
```
name: projectManager
auth: OAuth
endpoints:
 projects:
```
