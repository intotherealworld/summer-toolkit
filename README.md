# summer-toolkit

The toolkit for ths Summer(https://github.com/intotherealworld/summer). 
However, it is not only for the summer, then you can use it for your FastAPI base applications if you comply with a little rule for RouterScanner.

summer-toolkit provides several helping modules.
- RouterScanner: scan and include APIRouters which comply with the naming rule automatically
- SimpleJinja2Templates: find the template's absolute path with just a template directory name
- Environment: properties and phase management module. It can manage properties each deployment phase separately

## Installation
```shell
pip install git+https://github.com/intotherealworld/summer-toolkit.git
```

## Modules

### RouterScanner
filename pattern:
```
# "router" is cutomizable.
*_router.py
```
coding convention
```
# The part of asterisk(*) must be the same.
*_router = APIRouter(tags=...)
```
example
```
root_router.py

from summer_toolkit.framework.router_scanner import RouterScanner

root_router = APIRouter(tags=['root'])
```

### SimpleJinja2Templates
```
from summer_toolkit.framework.simple_jinja2_templates import SimpleJinja2Templates

# Just use like this, if the directory name for the templates is 'templates'
templates = SimpleJinja2Templates()

# specify the directory name
templates = SimpleJinja2Templates(directory='directory_name')
```
example
> An example is in the [root_router.py](https://github.com/intotherealworld/summer/blob/main/summer/root_router.py)

### Environment
```
from summer_toolkit.utility.environment import Environment

env = Environment()
title = env.get_props('summer.docs.title')
```
Setting deployment phase
```
# Environment Variable
SUMMER_DEPLOYMENT_PHASE=your_phase

# The file name of properties must be equal to the value of environment variable.
properties-your_phase.yml
```
If there are no environment variable named 'SUMMER_DEPLOYMENT_PHASE', only the properties.yml is used. The default properties are merged with the phase properties. A phase property which has the same name with a default property overrides it.
