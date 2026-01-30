
# Python - Django Application

1. Install Dependency

```

# Needed to monitor the application
pip install elastic-apm 

# Needed to monitor application system resource usage
pip install psutil  

```

2. Configure app settings

```

# add in the following in install section

INSTALLED_APPS = [
'elasticapm.contrib.django',
....
]

# add in the following in middleware section

MIDDLEWARE = [
'elasticapm.contrib.django.middleware.TracingMiddleware',
...
]


```

3. Configure the Environment Variables

```

ELASTIC_APM_SERVICE_NAME=
ELASTIC_APM_SERVER_URL=http://localhost:8200/<profile_key>
ELASTIC_APM_ENVIRONMENT=

```

> [! IMPORTANT]
> If application needs to run in debug mode then remove any other line stating following:
> 
> 	DEBUG = True
> 	
> Instead, replace with following:
> 
> 	
> 	ELASTIC_APM = { "DEBUG": True}
> 	

# Python - Flask Application

1. Install Dependency

```

# Needed to monitor the application
pip install elastic-apm flask

# Needed to monitor application system resource usage
pip install psutil 

```

2. Configure app settings

```

# import following

from elasticapm.contrib.flask import ElasticAPM
import os

# .....  

app = Flask(__name__)

# ..... 

apm = ElasticAPM(app)


```

3. Configure the Environment Variables

```

ELASTIC_APM_SERVICE_NAME=
ELASTIC_APM_SERVER_URL=http://localhost:8200/<profile_key>
ELASTIC_APM_ENVIRONMENT=
ELASTIC_APM_ENABLED=

```




