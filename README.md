<p align="right">
  <img src="https://img.shields.io/badge/MicroAI_AM_agent-4.2.5_-green" alt="Static Badge">
</p>
<br />
<p align="center">
  <img src="./docs/images/microai-logo.png" alt="MicroAI Logo" width="250">
</p>

<h3 align="center">MicroAI Application Performance Monitoring</h3>

<p align="center">
  MicroAI Application Performance Monitoring is an Edge-native AI platform that embeds and trains on application’s performance during the runtime, alerts if performance degradation is detected and pinpoints the underlying causes.
</p>

<p align="center">
  This guide will help you <strong>install</strong>, <strong>configure</strong>, and <strong>validate</strong> the MicroAI Application Performance Monitoring agent, ensuring it operates correctly and securely. No technical expertise is required—just follow the steps carefully, and you'll have the agent up and running in no time!
</p>


## Table of Contents

- [Installation](#installation)
- [Validation](#Validation)
- [Configurations](#configurations)
- [Features](#features)
- [Troubleshooting](#troubleshooting)
- [License](#license)
- [Contact](#contact) 

## Installation

Follow these steps below to install MicroAI Application Monitoring on your system. The installation process varies depending on your operating system and architecture. 

Determine your Operating system and architecture [here](docs/Detect_OS_Arch.md) and Packages are available [here](docs/Packages.md)

### 📖 Installation Instructions

> Side Note - Ensure Docker is installed and running on your system before executing the commands. For complete docker installation guide, please visit https://docs.docker.com/engine/install/
> 
> MicroAI License is required to run this agent. Get a trial license [here](docs/Registration-Instructions.md) or Please access this [guide](docs/Launchpad.md) page to setup account.

### Step 1: Set Up the Agent
##### For Debian/Ubuntu-based images

> 1. Installs dependencies needed to download, extract, and run MicroAI Application Monitoring Agent

```

RUN apt-get update && apt-get install -y \
    curl \
    tar \
    wget \
    pkg-config \
    build-essential \
    tcl
    
```

##### For CentOS/RedHat-based images

> 1. Installs dependencies needed to download, extract, and run MicroAI Application Monitoring Agent

```

RUN yum curl tar gzip \
    && yum groupinstall -y "Development Tools" \
    && yum clean all
```

##### Java Based Application


> 1. Downloads, extracts, cleans up, and provide permissions to run MicroAI Application Monitoring Agent
> 2. Sets Environment variables that are needed for MicroAI Application Monitoring Agent and Application to communicate
> 	1. Make sure to replace **<actual_package>** with the value of the application package
> 		- Example - com.sample.demo_app
> 3. EntryPoint to start the Apps in the container. 
> 	2. Make sure to replace **<application_name>** with the name of the actual application
> 		- Example - demo_app


```

# Step 2
RUN curl -L -o MicroAI_AM_agent.tar.gz https://maicdn.micro.ai/MicroAI_AM_Agent/MicroAI_AM_agent_4.2.0-linux-amd64.tar.gz && \
    tar -xzvf MicroAI_AM_agent.tar.gz && \
    chmod +x MicroAI_AM_agent/lib/scripts/setup.sh && \
    ./MicroAI_AM_agent/lib/scripts/setup.sh 

# Step 3
ENV ELASTIC_AGENT_PATH=/MicroAI_AM_agent/lib/elastic/java/elastic-apm-agent-1.55.1.jar
ENV MICROAI_AM_AGENT_HOST=http://127.0.0.1:8200
ENV MICROAI_AM_JAVA_PACKAGES=<actual_package>

# Step 4
ENTRYPOINT ["/bin/bash", "-c", "./MicroAI_AM_agent/bin/main & /start.sh <application_name>"]


```


##### **Environment File**


```
MICROAI_AM_ENABLE_AGENT=true
MICROAI_AM_ENABLE_LAUNCHPAD_DATA=true
MICROAI_AM_ENVIRONMENT=
MICROAI_AM_PROFILE_KEY=
MICROAI_AM_TRAINING_ROWS=500
MICROAI_AM_IS_BUILD_MODEL=false
MICROAI_AM_OBSERVATION_WINDOW_MINUTES=5
MICROAI_AM_EMAIL_HOST=
MICROAI_AM_EMAIL_PORT=
MICROAI_AM_EMAIL_USERNAME=
MICROAI_AM_EMAIL_PASSWORD=
MICROAI_AM_EMAIL_FROM=
MICROAI_AM_EMAIL_TO=
MICROAI_AM_EMAIL_TRANSACTION_BASE_URL=https://cloud1-icedata.micro.ai
MICROAI_AM_EMAIL_ICONS_BASE_URL=https://micro.ai
MICROAI_AM_FEED_INFO_BASE_URL=https://cloud1-api.micro.ai
MICROAI_AM_ALERT_MODIFIER=0.5
MICROAI_AM_EMAIL_ALERT_LEVELS=critical,high,medium,low,info
MICROAI_AM_ENABLE_ON_ALERT=true
MICROAI_AM_ALERT_DATA_CAPTURE_DURATION_MINUTES=15
MICROAI_AM_SEND_AGGREGATE_EVERY_N_MIN=60

```


**Script File - Must be included and named as start.sh**

> Make sure to update the Jar File Name to actual application jar file. **"demo-0.0.1-SNAPSHOT.jar"**


```

#!/bin/bash

set -e

SERVICE="$1"

echo "$(date -Is) startup service $SERVICE"


check_env_vars() {
    REQUIRED_ENV_VARS=("MICROAI_AM_ENVIRONMENT" "MICROAI_AM_PROFILE_KEY" "ELASTIC_AGENT_PATH" "MICROAI_AM_ENABLE_AGENT")
    if [ -z "$SERVICE" ]; then
        SERVICE="DEFAULT_APP_NAME_$HOSTNAME"
    fi
    for VAR in "${REQUIRED_ENV_VARS[@]}"; do
        if [ -z "${!VAR}" ]; then
            echo "Error: Missing required environment variable: $VAR"
            return 1
        fi
    done
    return 0
}

if check_env_vars && $MICROAI_AM_ENABLE_AGENT == true; then
    echo "$(date -Is) Attaching MicroAI Agent"
    MICROAI_AM_AGENT_URL="$MICROAI_AM_AGENT_HOST/$MICROAI_AM_PROFILE_KEY"
    MICROAI_OPS="-javaagent:$ELASTIC_AGENT_PATH 
            -Delastic.apm.server_url=$MICROAI_AM_AGENT_URL 
            -Delastic.apm.environment=$MICROAI_AM_ENVIRONMENT 
            -Delastic.apm.service_name=$SERVICE
            -Delastic.apm.application_packages=$MICROAI_AM_JAVA_PACKAGES"
else
    MICROAI_OPS=""
    echo "$(date -Is) MicroAI Agent not attached"
fi


exec java -XX:+UseG1GC $JAVA_OPTS $MICROAI_OPS -jar demo-0.0.1-SNAPSHOT.jar /config/application.properties



```

##### AspDotNet Based Application


> 1. Downloads, extracts, cleans up, and provide permissions to run MicroAI Application Monitoring Agent
> 2. Sets Environment variables that are needed for MicroAI Agent and Application to communicate
> 3. EntryPoint to start the Apps in the container. Make sure to replace **"applicationName"** with the name of the actual application.
>Update following variables:
> - ELASTIC_APM_SERVICE_NAME

```

# Step 2
RUN curl -L -o MicroAI_AM_agent.tar.gz https://maicdn.micro.ai/MicroAI_AM_Agent/MicroAI_AM_agent_4.2.0-linux-amd64.tar.gz && \
    tar -xzvf MicroAI_AM_agent.tar.gz && \
    chmod +x MicroAI_AM_agent/lib/scripts/setup.sh && \
    ./MicroAI_AM_agent/lib/scripts/setup.sh 

# Step 3
ENV ELASTIC_APM_SERVICE_NAME=Dotnet-Test-App \
	CORECLR_PROFILER={FA65FE15-F085-4681-9B20-95E04F6C03CC} \ 
	CORECLR_PROFILER_PATH=/MicroAI_AM_agent/lib/elastic/aspdotnet/libelastic_apm_profiler.so \
	ELASTIC_APM_PROFILER_HOME=/MicroAI_AM_agent/lib/elastic/aspdotnet \
	ELASTIC_APM_PROFILER_INTEGRATIONS=/MicroAI_AM_agent/lib/elastic/aspdotnet/integrations.yml

# Step 4
ENTRYPOINT ["/bin/bash", "-c", "/MicroAI_AM_agent/bin/main -debug -crypto=MICROAI_123 & dotnet applicationName"]

```


**Environment File - Things to include**

> Update following variables:
> - MICROAI_AM_EMAIL_TO
> - ELASTIC_APM_SERVER_URL=http://127.0.0.1:8200/{profile_key} from Launchpad
> - ELASTIC_APM_ENVIRONMENT

```

# MicroAI Config
CORECLR_ENABLE_PROFILING=1
ELASTIC_APM_ENVIRONMENT=TestEnvironment
ELASTIC_APM_SERVER_URL=http://127.0.0.1:8200/06a81a4fb98d149f2d31c68828fa6e

MICROAI_AM_ENABLE_AGENT=true
MICROAI_AM_ENABLE_LAUNCHPAD_DATA=true
MICROAI_AM_ENVIRONMENT=
MICROAI_AM_PROFILE_KEY=
MICROAI_AM_TRAINING_ROWS=500
MICROAI_AM_IS_BUILD_MODEL=false
MICROAI_AM_OBSERVATION_WINDOW_MINUTES=5
MICROAI_AM_EMAIL_HOST=
MICROAI_AM_EMAIL_PORT=
MICROAI_AM_EMAIL_USERNAME=
MICROAI_AM_EMAIL_PASSWORD=
MICROAI_AM_EMAIL_FROM=
MICROAI_AM_EMAIL_TO=
MICROAI_AM_EMAIL_TRANSACTION_BASE_URL=https://cloud1-icedata.micro.ai
MICROAI_AM_EMAIL_ICONS_BASE_URL=https://micro.ai
MICROAI_AM_FEED_INFO_BASE_URL=https://cloud1-api.micro.ai
MICROAI_AM_ALERT_MODIFIER=0.5
MICROAI_AM_EMAIL_ALERT_LEVELS=critical,high,medium,low,info
MICROAI_AM_ENABLE_ON_ALERT=true
MICROAI_AM_ALERT_DATA_CAPTURE_DURATION_MINUTES=15
MICROAI_AM_SEND_AGGREGATE_EVERY_N_MIN=60

```

---


### Step 2: Activate your License

Activate your license and retrieve your license key on [MicroAI Launchpad](https://launchpad.micro.ai/activate/apmtrial). See [activation walkthrough](docs/Registration-Instructions.md) for guided steps.

## Validation

After starting container, use the following steps to ensure the agent is running correctly:

1. **Check if the Agent has started**:

   ```bash
   docker logs <container_name>
   ```

	>Look for these messages as this will indicate a successful start of an Agent

	```
	 __  __ _                        _____  TM
	|  \/  (_)                 /\   |_   _|
	| \  / |_  ___ _ __ ___   /  \    | |  
	| |\/| | |/ __| '__/ _ \ / /\ \   | |  
	| |  | | | (__| | | (_) / ____ \ _| |_ 
	|_|  |_|_|\___|_|  \___/_/    \_\_____|
	Closehandler set
	AtomML+ Application Performance Monitoring v1.0.0
	Config Parsed
	```

2. **Verify logs for errors**:
	- Logs are available inside the container in this Path: 
		``` <Container_Working_Dir_Path>/MicroAI_AM_agent/data/logs ```
	- Main logging file is the one labeled as `main`
	
   ```bash
   cat <path>/microai-main-{auto-generated-date}.log
   ```

If all checks pass, the agent is successfully configured and operational!


## Configurations

To customize your agent settings, refer to the [Configurations Guide](docs/Configurations.md).

If you wish to view your manage profile, or view dashboards follow this [guide](docs/Launchpad_Setup.md).

## Features

Take a peek at our [feature page](docs/Feature-List.md) for current features available with our agent.

## Troubleshooting

If you encounter issues, try these solutions:

### Issue:  Where are the log files?

>Inside the container path: `{Working-Directory}/MicroAI_AM_agent/data/logs`

- Solution:
  ```bash
  docker exec -ti <container_name> bash
  cd <Working-Directory>/MicroAI_AM_agent/data/logs
  ```


For further assistance, contact [**support@micro.ai**](mailto\:support@micro.ai).

---

### License

See [Software Licensing Agreement](License.txt) for more details.

---

## Contact

- **Company:** MicroAI™
- **Website:** [https://smartapm.micro.ai/](https://smartapm.micro.ai/)
- **Email:** [support@micro.ai](mailto\:support@micro.ai)

