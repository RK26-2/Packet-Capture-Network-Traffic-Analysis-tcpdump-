# Packet-Capture-Network-Traffic-Analysis-tcpdump-

## Executive Summary 
This lab demonstrated my ability to capture and analyse live network traffic using `tcpdump` on a Linux system. Network packet analysis is a core skill in SOC and incident response roles, as it enables analysts to identify suspicious activity, investigate incidents, and understand attacker behaviour at the network level. 

## Scenario 
I acted as a network analyst who needed to use `tcpdump` to capture and analyse live network traffic from a Linux virtual machine. 

## Key Tasks Completed 
* **Identified** network interfaces using `ifconfig` and `tcpdump -D`.
* **Captured** and **analysed** live packets on `eth0`, interpreting TCP flags, TTL, TOS, and protocol details.
* **Captured** HTTP traffic to a pcap file using port filtering and background processing.
* **Analysed** captured packets using `-r`, `-v`, and `-X` flags for detailed inspection.

---

## Technical Walkthrough & Analysis

### 1. Traffic Capture
I captured data into a file called `capture.pcap` using the command `sudo tcpdump -i eth0 -nn -c9 port 80 -w capture.pcap &` and pressed Enter. Here, I told `tcpdump` to capture 9 packets of data (`-c9`) from interface `eth0`, but not to resolve IP addresses or ports to names using `-nn`, which wouldn't inform the attacker about the capture. I also indicated that it should filter only port 80. Then, I asked it to save (`-w`) the captured data to the file `capture.pcap`. Finally, I instructed the Bash shell to run the command in the background by using `&`.

In a later step, I verified that the packet had been captured by using the `ls -l` command, and then I filtered the captured packet data. Here, `-r` was used for reading the captured data, and `-v` for viewing detailed packet data. Finally, I used `-X` for extended packet data, as requested by the lab.

### 2. Packet Analysis
In the capture, I could see that `tcpdump` was listening on `eth0`, link-type EN10MB (Ethernet). The next line showed the timestamp `14:45:43.971211 IP`, followed by the protocol type, IP. Next, `-v` provided more details about the IP packet fields, such as TOS, TTL, offset, flags, and the internal protocol type (e.g., TCP (6)), as well as the length of the outer packet in bytes. 

The following section showed the communication from `internal.39152` to `3366a0da4d0c.5000`. Following that, the packet identified TCP flags; flag 'P' represented push and the period indicated it was an ACK flag, meaning that the packet was pushing out data.

---

## Lessons Learned & Conclusion 
This lab reinforced the importance of precise packet filtering in a SOC environment. Using `-nn` prevented DNS resolution during the capture, which reduced noise and avoided alerting potential attackers. Background processing with `&` allowed for simultaneous traffic generation and capture, while `-X` revealed hex and ASCII payload data useful for identifying malicious content. Overall, this lab strengthened my practical network forensics skills, which are highly applicable to incident investigation and threat detection.


## The pdf document link is here:

Report 👉 [tcpdump_lab_packet_capture_Linux_CLI.pdf](/tcpdump_lab_packet_capture_Linux_CLI.pdf)

## Images

Screenshots 👉  [Images](/images)
