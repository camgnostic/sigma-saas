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
 - Users log in with google OAuth
 - Two categories of user: project managers and contributors
 - Projects belong to one or more project managers
 - Tasks belong to projects
 - Subtasks belong to tasks
 - Tasks/subtasks have a short and long description, start date, due date, and progress updates
 - Tasks/subtasks are assigned to contributors/project managers
 - Each user has a to-do list page, calendar page, and the ability to update their tasks.
 - Project managers have a global view of their projects, view per project, and the ability to create/assign tasks/subtasks to contributors.

## Option 1 (URL-based spec):
```
name: projectManager
auth: OAuth
endpoints:
 projects:
```
_specify each http method? permissions? expected response?_

## Option 2 (resource-based spec):
```
name: projectManager
auth: OAuth
defaults:
 charfield:
  length: 40
resources:
 User:
  fields:
   first_name: charfield
   last_name: charfield
   username: charfield
    unique
   user_level:
    choices:
     ProjectManager
     Contributor
 Project:
  fields:
   name:
    length: 40
    good: To-Do List
   owner:
    User
```
_how to specify user must be projectmanager flagged?_

## Option 3 (frontend-based spec):
```
name: projectManager
auth: OAuth
splash:
 anonymous:
  actions:
   login
 user:
  components:
   dashboard
dashboard:
 projectManager:
  actions:
   calendar
  components:
   project-list
 contributor:
  actions:
   calendar
  components:
   task-list
project-list:
 components:
  repeated:
   project-summary
task-list:
 components:
  repeated:
   task-summary
project-summary:
 object: project
 actions:
  project-detail
 fields:
  project:
   name
   owner:
    name
 components:
  repeated:
   task-summary
```
_how to indicate that only tasks assigned to this project should be displayed?_

## Option 4 (actions-based-spec):
```
name: projectManager
auth: OAuth
initial:
 test: user.logged_in
 false:
  login
 true:
  test: user.user_type
  projectManager:
   view:
    project-list
   go:
    calendar
  contributor:
   view:
    task-list
   go:
    calendar
```
_how is this different from option 3?  Is it worth exploring both to get to "actions" like update and find differences?_


## Swagger output:
The swagger output for any of the four options should be identical (same toy project):
```
swagger: '2.0'
info:
  version: "1.0.0"
  title: "projectManager"
paths:
  /projects:
    get:
      description: Gets `Project` objects.
      operationId: findProjects
      produces:
        - application/json
      responses:
        '200':
          description: projects response
          schema:
            title: ArrayOfProjects
            type: array
            items:
              $ref: '#/definitions/project'
        default:
          description: unexpected error
          schema:
            $ref: '#/definitions/errorModel'
    post:
      description: Creates a new `Project` object
      operationId: addProject
      produces:
        - application/json
      parameters:
        - name: project
          in: body
          description: project to add to the project list
          required: true
          schema:
            $ref: '#/definitions/newProject'
      responses:
        '201':
          description: project created successfully
          schema:
            $ref: '#/definitions/project'
        default:
          description: unexpected error
          schema:
            $ref: '#/definitions/errorModel'
  /projects/{id}:
    get:
      description: returns a single `Project` by ID, if the user has access to the project
      operationId: findProjectById
      produces:
        - application/json
      parameters:
        - name: id
          in: path
          description: id of project to fetch
          required: true
          type: integer
          format: int64
      responses:
        '200':
          description: project response
          schema:
            $ref: '#/definitions/project'
        default:
          description: unexpected error
          schema:
            $ref: '#/definitions/errorModel'
    put:
      description: updates details of a particular `Project`
      operationId: updateProject
      produces:
        - application/json
      parameters:
        - name: id
          in: path
          description: id of project to update
          required: true
          type: integer
          format: int64
        - name: name
          description: updated project name
          required: false
          type: string
        - name: owner
          description: updated project owner
          required: false
          type: int
          format: int64
      responses:
        '200':
          description: project response
          schema:
            $ref: '#/definitions/project'
        default:
          description: unexpected error
          schema:
            $ref: '#/definitions/errorModel'
    delete:
      description: deletes a specified `Project`
      operationId: deleteProject
      produces:
        - application/json
      parameters:
        - name: id
          in: path
          description: id of project to fetch
          required: true
          type: integer
          format: int64
      responses:
        '204':
          description: successfully deleted
        default:
          description: unexpected error
          schema:
            $ref: '#/definitions/errorModel'
```
