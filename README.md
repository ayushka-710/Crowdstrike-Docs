# Log Ingestion or Log Forwarding Architecture
## Log_Management_SIEM:
This document outlines all the steps and procedures required to forward logs using rsyslog to the Humio Log Collector (CrowdStrike) and ultimately to the CrowdStrike Cloud.

### Step-By-Step Procedures:
1. Enable **ForwardToSyslog=yes** in **journald.conf**. Reference image **Screenshot 2025-05-27 at 11.19.32.png**
   **(pod_deleted_SIEM(folder))**. System level logs will be stored in **/var/log/syslog or /var/log/messages**
   
2. Provide IP and port of a humio-log-collector within a file **/etc/rsyslog.conf**. To redirect syslog to humio-log-collector. Reference       image **Screenshot 2025-07-03 at 16.20.04.png**
   - *.* @@<humio-log-collector-IP>:<port>
   - @ = Send it via UDP
   - @@ = Send it via TCP
   
3. Create a config file like **/etc/rsyslog.d/crowdstrike.conf** to send third party application logs to **humio-log-collector**. Reference     image **Screenshot 2025-06-30 at 15.29.21.png**. The config file consists of content to exclude or drop unwanted messages from the log       source before sending towards **humio-log-collector**.
   
4. Download logscale (humio-log-collector) from Crowdstrike Console. Path **Support and resources > Tool Downloads > LogScale Collector For     Ubuntu** (choose as per your OS).

5. Extract all the files and folder of humio-log-collector and edit within the path **/etc/humio-log-collector/config.yaml**. Reference         image **Screenshot 2025-05-27 at 11.12.16.png (pod_deleted_SIEM)**.

6. Check if a process is listening on specific <port> or not. Use tcpdump to check whether the packets has be collected by humio-log-           collector or not within a specific port. Reference image **Screenshot 2025-05-27 at 11.23.08.png** and **2025-06-28_21-20-16-156.png**.
   - netstat -tulnap | grep <port>
   - tcpdump -i any port <port-number> -A (To check whether the packets has been collected or not.)

7. **2025-06-28_21-20-19-863.png** (This image displays the logs that are present in **testlog** file in source side.)

8. **2025-06-28_21-20-16-156.png** (This images displays the packets that have been collected by humio-log-collector in destination side.)

9. **2025-06-28_21-20-19-038.png** (This image confirms that the logs have been successfully sent to the cloud and are accessible in the        CrowdStrike console.)

10. **Screenshot 2025-06-27 at 16.04.13.png** (This is the log we are going to exclude or drop it from source side(unwanted logs).)

11. **2025-06-28_21-20-17-990.png** (This config file consists of content that help to drop the unwanted messages.)

12. **2025-06-28_21-20-20-871.png** (This image clarifies that the logs has been dropped.)

### To prevent unwanted logs from reaching the CrowdStrike cloud, we need to drop them by updating the log collector configuration file.

1. **Screenshot 2025-06-30 at 15.29.21.png** (Sending logs from source side to destination side.)

2. **Screenshot 2025-07-03 at 16.20.04.png** (if port is changed need to change within this conf file also.)

3. **Screenshot 2025-06-30 at 15.25.55.png** (need to create a config file in destination side in order to collect the logs send from source    side and store the logs within a file.)

4. **Screenshot 2025-06-30 at 15.24.23.png** (need to modify the config file of humio-log-collector if you want to exclude or drop logs from    being collected by humio-log-collector. Need to add **transforms** block.)


## Pod_FQL_SIEM:
 This folder contains images that illustrate the syslog-based log forwarding pipeline and architecture, along with the use of **Falcon Query  Language (FQL)** for security visibility and threat detection in **Kubernetes orchestration environments**.
   
