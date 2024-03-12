
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
