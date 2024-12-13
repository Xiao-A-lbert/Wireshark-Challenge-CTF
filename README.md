# Wireshark Challenge CTF

<h2>Description</h2>
In this wireshark challenge, I dived into a challenge pcap to look for http get requests to an "image/gif" which was a trojan.pikabot that uses dns tunneling to a C2 server.  


<h2>Languages and Utilities Used</h2>

- <b>wireshark</b>
- <b>linux CLI</b>


<h2>Environments Used </h2>

- <b>Unbuntu</b> 

<br />
<br />
Challenge prompt.

![1) challenge prompt](https://github.com/user-attachments/assets/9d5e4701-91c9-4fdb-a5fe-31fbb4b366de)

<br />
<br />
First domain queried and assocaited ip address. 

![2) q2 3](https://github.com/user-attachments/assets/cbcef7a6-30f4-4642-abb8-17c15e1e8aad)

<br />
<br />  
Filtering for http apckets, shows 8 packets, path to access web server from victim shown by right click GET request > follow http stream. Shows the victim retreived an "image/gif" with MZ magic bytes file signature. 

![3) q 5-7](https://github.com/user-attachments/assets/44373abd-4000-4d50-a707-cdea64be0472)

<br />
<br />
Looking at the 2nd packet under http, the user-agent shows the use of windows powershell used to download the file. 

![4) q 8](https://github.com/user-attachments/assets/6bce4a5f-a21b-499c-8461-74893bf8f1f9)

<br />
<br />
Exporting the http object "image/gif" and generating a sha256 hash. 

![5) sha256 hash](https://github.com/user-attachments/assets/d802b12a-b4f1-4a47-a96c-3407c25737d3)

<br />
<br />
Virustotal shows 60 vendor flags with a tag of trojan pikabot for the "image/gif"

![6) virustotal tag](https://github.com/user-attachments/assets/01649dcf-d69b-4ce4-b6e3-028ac7a8affa)

<br />
<br />
Looking at protocol hierarchy stats shows 37.5% of of all packets are from DNS. 

![7) dns majority udp](https://github.com/user-attachments/assets/6ba92c62-6ad3-4d4f-b9c7-5463a3bf6737)

<br />
<br />  
Filtering for DNS and scrolling down shows stealsteel[.]net frequently queried. 

![8) stealsteel](https://github.com/user-attachments/assets/75098a76-605a-4a0f-baf7-e95716b19d6c)

<br />
<br />
This attack type from MITRE research is called DNS tunnelling. Instead of using DNS requests and replies to perform legitimate IP address lookups, malware uses it to implement a command and control channel with its handler.

![9) dns tunneling](https://github.com/user-attachments/assets/3457d1b7-bd20-40a8-b0b7-8edfaea32c45)

<br />
<br />
