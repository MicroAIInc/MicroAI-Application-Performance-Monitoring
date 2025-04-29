# 📦 Software Downloads

Welcome to the **official download page** for our software. Below, you'll find download links for **Linux (x64, ARM, ARM64)** and **Windows (x64)**.

---

## 🐧 Linux Downloads
| Version | Architecture | Tar File                                                                                       |
| ------- | ------------ | ---------------------------------------------------------------------------------------------- |
| 3.0.0   | **x64**      | [Download](https://maicdn.micro.ai/MicroAI_AM_Agent/MicroAI_AM_agent_3.0.0-linux-amd64.tar.gz) |


> **Note:** To monitor containerized applications:
#### Key Considerations
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
