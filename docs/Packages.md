# 📦 Software Downloads

Welcome to the **official download page** for our software

---

## 🐧 Linux Downloads
| Version | Architecture | Tar File                                                                                       |
| ------- | ------------ | ---------------------------------------------------------------------------------------------- |
| 4.1.1   | **x64**      | [Download](https://maicdn.micro.ai/MicroAI_AM_Agent/MicroAI_AM_agent_4.1.1-linux-amd64.tar.gz) |

## Release Notes

### Version 4.1.1 <sup><span style="background-color:#28a745;color:white;padding:2px 6px;border-radius:3px;font-size:0.8em;">Stable</span> </sup>  
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
