# Vision:
A cloneable repo that sets up:
 - An API specification
 - A Django-based RESTful API
 - An Angular frontend

## API Specification
The API specification purpose is two-fold:
 - Documentation
 - Testing
### Documentation
The API specification should produce a (?) Swagger document for further development and for reference.
Documentation should be easily navigable and complete, auto-generated from the provided specification file.
### Testing
Tests should be generated from specification file that test the RESTful back-end.

### Implementation
After cloning the SAAS-in-a-box repo, the user provides a (?) YAML specification file, and runs "build.py".  Build.py:
 - generates Swagger documentation for the API
 - generates a Django/DRF project (including pip requirements file) meeting specifications
   - generates unit tests within the Django project to test models/serializers against specification file constraints
 - generates an angular project directory with a one-page angular app to access the API
 - generates a test-harness directory which externally tests the DRF API through localhost http requests

# Progress:
 - [ ] Specification file format [started here](specifications.md)
 - [ ] Build.py consumes specification file and produces swagger api spec
 - [ ] Build.py consumes specification file and produces django project
 - [ ] Build.py consumes specification file and produces test harness
 - [ ] Build.py consumes specification file and produces angular project
