
PowerShell Command
Windows
I have the issue:
TLS Version Compatibility: There could be compatibility issues with the TLS version used by PowerShell. You can try forcing a specific TLS version by setting the [System.Net.ServicePointManager]::SecurityProtocol property before making the request. For example:
```
[System.Net.ServicePointManager]::SecurityProtocol = [System.Net.SecurityProtocolType]::Tls12
Invoke-WebRequest -Uri 'https://airflow.apache.org/docs/apache-airflow/2.8.3/docker-compose.yaml' -OutFile 'docker-compose.yaml'

```
Unix:
```
curl -LfO 'https://airflow.apache.org/docs/apache-airflow/2.7.3/docker-compose.yaml'
```
It seems you're using PowerShell, and the -p option with mkdir is not recognized in PowerShell as it is in Unix-based systems like Linux or macOS.

To create multiple directories with PowerShell, you can use the New-Item cmdlet with the -ItemType Directory parameter. Here's how you can do it:
'''
New-Item -ItemType Directory -Path ./dags -Force
New-Item -ItemType Directory -Path ./logs -Force
New-Item -ItemType Directory -Path ./plugins -Force
New-Item -ItemType Directory -Path ./config -Force

'''
This will create the dags, logs, plugins, and config directories in the current directory. The -Force parameter is used to create the directories even if they already exist, without prompting for confirmation.

Alternatively, if you prefer a single command to create multiple directories, you can concatenate the directory paths using semicolons (;) and then pass them to New-Item:
```
New-Item -ItemType Directory -Path './dags', './logs', './plugins', './config' -Force
```

