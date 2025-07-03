# Log_Management_SIEM:
This document outlines all the steps and procedures required to forward logs using rsyslog to the Humio Log Collector (CrowdStrike) and ultimately to the CrowdStrike Cloud.

## Step-By-Step Procedures:
1. Enable **ForwardToSyslog=yes** in **journald.conf**. Reference image **Screenshot 2025-05-27 at 11.19.32.png**
   **(pod_deleted_SIEM(folder))**. System level logs be stored in **/var/log/syslog or /var/log/messages**
   
2. Provide IP and port of a humio-log-collector within a file **/etc/rsyslog.conf**. To redirect syslog to humio-log-collector. Reference       image **Screenshot 2025-07-03 at 16.20.04.png**
   - *.* @@<humio-log-collector-IP>:<port>
   - @ = Send it via UDP
   - @@ = Send it via TCP
   
3. Create a config file like **/etc/rsyslog.d/crowdstrike.conf** to send third party application logs to **humio-log-collector**. Reference     image **Screenshot 2025-06-30 at 15.29.21.png**. The config file consists of content to exclude or drop unwanted messages from the log       source before sending towards **humio-log-collector**.
   
4. Download logscale (humio-log-collector) from Crowdstrike Console.          
