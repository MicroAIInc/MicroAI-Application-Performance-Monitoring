# 📦 Software Downloads

Welcome to the **official download page** for our software

---

## 🐧 Linux Downloads
| Version | Architecture | Tar File                                                                                       |
| ------- | ------------ | ---------------------------------------------------------------------------------------------- |
| 4.1.5   | **x64**      | [Download](https://maicdn.micro.ai/MicroAI_AM_Agent/MicroAI_AM_agent_4.1.5-linux-amd64.tar.gz) |
| 4.1.3   | **x64**      | [Download](https://maicdn.micro.ai/MicroAI_AM_Agent/MicroAI_AM_agent_4.1.3-linux-amd64.tar.gz) |
| 4.1.2   | **x64**      | [Download](https://maicdn.micro.ai/MicroAI_AM_Agent/MicroAI_AM_agent_4.1.2-linux-amd64.tar.gz) |
| 4.1.1   | **x64**      | [Download](https://maicdn.micro.ai/MicroAI_AM_Agent/MicroAI_AM_agent_4.1.1-linux-amd64.tar.gz) |

## Release Notes

### Version 4.1.5 <sup><span style="background-color:#28a745;color:white;padding:2px 6px;border-radius:3px;font-size:0.8em;">Stable</span> </sup>  
**Release Date:** Aug 29, 2025  

#### 🚀 What's New
- Enhanced Email Alerts: Email notifications now fixed with trace data for improved visibility and diagnostics.
- Agent Vulnerability Fixes: Addressed multiple security vulnerabilities in the agent to improve overall system resilience and safety.

>Update following parameters:
>
>MICROAI_AM_EMAIL_ICONS_BASE_URL=https://micro.ai
>ELASTIC_AGENT_PATH=/MicroAI_AM_agent/lib/elastic/java/elastic-apm-agent-1.55.1.jar


### Version 4.1.3   
**Release Date:** Aug 05, 2025  

#### 🚀 What's New
- Resolved an issue where email notification links were directing users to a blank data page.
- Addressed a bug in the data ingestion pipeline to ensure consistent and accurate data processing.

### Version 4.1.2   
**Release Date:** July 23, 2025  

#### 🚀 What's New
- Introduced functionality to monitor application resource consumption
- Introduced monitoring for application running state, including detection of up, down, and recover state

### Version 4.1.1 
**Release Date:** July 3, 2025  

#### 🚀 What's New
- Added functionality to **adjust AI alert sensitivity**, enabling fine-tuned control based on user preference.  
- Introduced the ability to **customize alert severity**, enabling users to define which levels of alert severity they wish to receive.

---

## Key Considerations

> **Note:** To monitor containerized applications:
> 
- Ensure Docker is installed and running on your system before executing the commands. See [Docker docs](https://docs.docker.com/engine/install/).
- If you need to update the configuration file, you can mount the config directory using the `-v` option and add this to the commands below:  
  ```bash
  -v <absolute_path_to_config_directory_on_host_machine>:<working_dir_path>/MicroAI_AM_agent/config
  ```
- Similarly, to access logs from the host machine, mount the log directory as follows:  
  ```bash
  -v <absolute_path_to_log_directory_on_host_machine>:<working_dir_path>/MicroAI_AM_agent/data/logs
  ```
- Only supports system with GLIBC 2.27 or newer
