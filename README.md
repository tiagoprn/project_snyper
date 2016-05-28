# Project Snyper

The motivation for this project is to create small tools that do one thing and
do it well, the UNIX's philosophy style. They have a REST API so
their methods can be called through curl and web/native UIs using React/React 
native.

The project name derives from "snipers" - shooters with an impressive aim that
reach their target successfully using just one shot (as UNIX tools are meant to
be).

Each tool will be named "bullet". Each bullet must have the simplest and least 
code possible to do the work it is designed to do. It must also have tests 
using py.test, and be exposed as a microservice on a REST API 
with the help of swagger.  

These will be the **first "wave" of bullets** to be developed: 

- **markee**: CRUD links (bookmarks) on a Mongo collection, supporting 
optional tags;

- **keepee**: CRUD notes on a Mongo collection, supporting optional tags 
and versioning;

- **timee**: a simple time tracker, supporting "start/top" 
and projects as "tags".

And these will be the next ones:

- gettee: Download the contents of a link (just the html text and images - 
if it has "next" pages it will have all the text);

- mailee: Send content to e-mail recipients;

- birdee: create/retrieve contents from a twitter account

This will allow the development of new more complex tools on top of these ones 
(as other git repositories, not inside this one). E.g.: 

- A blog app that uses "keepee" to get/create contents and "birdee" to post a
    link to it on Twitter when it is published.

- A poor man's "wallabag" app where I use "markee", "gettee" and 
"mailee" to store/get the links on an e-mail account created specifically 
for that. I could also develop a Firefox browser extension to collect the links 
for this poor man's app.  

# Development notes

## Technologies: 

- python 3 (only), flask, gevent, uwsgi, nginx. If it scales enough, 
HAProxy load balancing to nginx instances. 

- marshmallow: Python library for validating input data against a schema,
  deserializing data to application objects (e.g. ORM objects), and serializing
application objects to simple types:
http://stevenloria.com/marshmallow-20-released/ - it can be used as a more
featureful alternative “json.dumps/loads”. 

- mongo (in conjunction with marshmallow below - will avoid MongoEngine unless
  marshmallow is not suitable for this task)

- yosai-project: Authentication, Authorization and Session Management:
  http://yosaiproject.github.io/yosai/ . As an alternative, I could develop
a bullet, using this schema: https://github.com/membership/membership.db (but
on MongoEngine). 

- swagger: to document the APIs. 


## Assumptions

### Code structure: 

- Although on the same repository umbrella, each bullet module must be 
inside its own directory(containing code, docs and the flask app). Keep in 
mind that this project is just an umbrella, so each bullet can be developed/
used independently. 
 
- Code that is shareable must be on a "commons" module under this main project 
directory.

### For the development of each bullet, follow this process: 

1) Inside the root directory, create a python module for the bullet 
containing the class for its functionality

2) Create py.test tests for the module

3) Create the flask app for the API (inside the module)
 
4) Create py.test tests for flask API

5) Integrate yosai for authorization

6) Add tests for the authorization to the Flask API tests of step "4".
