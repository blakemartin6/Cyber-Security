# Wireshark Capture: Nmap & HTTP Traffic to Metasploitable

## 🧪 Lab Overview

This lab demonstrates a basic packet capture of traffic between a Kali Linux machine and a vulnerable Metasploitable VM. The focus was on scanning the target with Nmap and capturing resulting network activity, including HTTP traffic over port 80.

## 🖥️ Environment Setup

- Attacker Machine: Kali Linux  
  - IP: 192.168.56.10
- Target Machine: Metasploitable 2  
  - IP: 192.168.56.11
- Network: VirtualBox Host-Only Adapter (vboxnet0)
- Isolation: Both VMs are isolated from the internet and host network

## 🔧 Steps Performed

1. Verified network connectivity between Kali and Metasploitable.
2. Launched Wireshark on Kali and began a capture on interface eth0.
3. Ran a full port Nmap scan from Kali to Metasploitable:
   sudo nmap -p- 192.168.56.11
4. Filtered Wireshark to display only HTTP traffic:
   tcp.port == 80
5. Opened a web browser on Kali and navigated to http://192.168.56.11 to generate HTTP traffic.
6. Stopped the capture and saved the .pcapng file.

## 📊 What Was Captured

- TCP SYN Scans (from Nmap): Evidence of Nmap probing port 80 with SYN packets
- TCP 3-Way Handshake: SYN → SYN/ACK → ACK between Kali and Metasploitable
- HTTP Requests: GET requests to the default web pages hosted on Metasploitable (e.g., Apache splash pages)
- Session Teardowns: RST flags sent by Nmap or browser to close the sessions

## 🔍 Key Wireshark Filters Used

- TCP Port 80 Filter:
  tcp.port == 80

- Follow TCP Stream: Used to inspect full request/response cycles

## 🧠 Learning Outcome

This exercise reinforced the following:
- Differentiating between SYN scans (-sS) and full connect scans (-sT)
- Identifying TCP session behavior in Wireshark
- Recognizing the structure of a 3-way handshake and HTTP traffic
- Understanding why it's critical to isolate vulnerable VMs like Metasploitable

## 📁 Related Files

- wireshark_http_capture.pcapng: Capture file showing traffic during scan and browsing
- README.md: This documentation
