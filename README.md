Trend Micro Vision One API to ELK Integration

**Overview**
This project integrates Trend Micro Vision One Workbench Alerts with the ELK Stack (Elasticsearch, Logstash, and Kibana) using Python.

The Python collector retrieves alerts from Trend Micro Vision One through REST APIs and forwards them to Logstash using UDP port 5515.


**Architecture**
Trend Micro Vision One Cloud │ │ HTTPS 443 ▼ Windows Python Collector │ │ UDP 5515 ▼ Logstash │ ▼ Elasticsearch │ ▼ Kibana Dashboard




**#Features**
Trend Micro Vision One API Integration
Python Alert Collector
Logstash UDP Ingestion
Elasticsearch Indexing
Kibana Dashboard Visualization
Automatic Alert Collection Every 5 Minutes
Duplicate Alert Prevention
Requirements
Windows Collector
Python 3.x
Visual Studio Code
Internet Access
ELK Server
Elasticsearch
Logstash
Kibana
Python Installation
Verify Python:

python --version
Configure API Key
Update:

API_KEY = "YOUR_API_KEY"
Replace with your own Trend Micro Vision One API key.

Run Collector
python "C:\Users\<USERNAME>\Desktop\SOC\SOC.py"
Expected:

Status: 200
Received 10 alerts
Sent 10 new alerts to ELK
Logstash Configuration
Location:

cd /etc/logstash/conf.d
nano trendmicro.conf
Input:

input {
  udp {
    port => 5515
    codec => json
  }
}
Logstash Validation
sudo /usr/share/logstash/bin/logstash \
--path.settings /etc/logstash \
--config.test_and_exit
Restart Logstash
sudo systemctl restart logstash
Verify Port
sudo ss -lunp | grep 5515
Expected:

0.0.0.0:5515
Elasticsearch Verification
List indices:

curl -k -u elastic:PASSWORD \
https://localhost:9200/_cat/indices?v
Document count:

curl -k -u elastic:PASSWORD \
https://localhost:9200/trendmicro-*/_count?pretty
Kibana Configuration
Create Data View:

Stack Management
→ Data Views
→ Create Data View
Name:

TrendMicro
Index Pattern:

trendmicro-*
Timestamp Field:

@timestamp
Discover Query
source:"trendmicro"
Dashboard Recommendations
Alerts by Severity
Alerts by Status
Investigation Status
Average Risk Score
Alert Trend
Recent Alerts Table
Scheduled Task
Trigger:

At Startup
or

At Logon
Program:

python
Arguments:





**"C:\Users\<USERNAME>\Desktop\SOC\SOC.py"**
**Project Status**
✅ Trend Micro API Connected

✅ Python Collector Operational

✅ Logstash Integration Completed

✅ Elasticsearch Indexing Successful

✅ Kibana Dashboard Functional

✅ Automated Collection Enabled
