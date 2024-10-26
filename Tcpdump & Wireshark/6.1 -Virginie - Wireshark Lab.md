# Wireshark Lab: Network Traffic Investigation

## Scenario Overview
In this scenario, I am a security analyst investigating traffic to a website. I analyzed a network packet capture file containing traffic data related to a user connecting to an internet site. Filtering network traffic using packet sniffers to gather relevant information is an essential skill for a security analyst.

### Objectives:
- Identify the source and destination IP addresses involved in this web browsing session.
- Examine the protocols used when the user makes the connection to the website.
- Analyze some data packets to identify the type of information sent and received by the systems that connect during the network data capture.

## Key Steps in the Process

### Step 1: Opening the Packet Capture File
1. Open the packet capture file using Wireshark.
2. Explore the basic Wireshark graphical user interface.
3. Open a detailed view of a single packet to examine the various protocol and data layers inside a network packet.
4. Apply filters to select and inspect packets based on specific criteria.
   
![Lab8step1](https://github.com/user-attachments/assets/162e7520-8352-4b9a-9550-2c779dedd3c6)


#### Key Packet Columns:
- **No.**: Index number of the packet in the capture file.
- **Time**: Timestamp of the packet.
- **Source**: Source IP address.
- **Destination**: Destination IP address.
- **Protocol**: Protocol contained in the packet.
- **Length**: Total length of the packet.
- **Info**: Information about the data in the packet (interpreted by Wireshark).

Packets are displayed in different colors, providing high-level visual cues to classify data types. For example, DNS traffic packets are shown in light blue, while TCP and HTTP protocol traffic packets are shown in green.

### Step 2: Filtering and Inspecting a Packet
Apply a basic filter to the network data to isolate specific traffic.

1. Enter the following filter in the text box to filter traffic associated with a specific IP address:
   
   `ip.addr == 142.250.1.139`
   
3. Double-click the first packet where the protocol is TCP. This opens a detailed view of the packet's structure.
4. Expand the following subtrees to examine the packet data:
   - **Frame**: Provides details about the overall network packet, including the frame length and arrival time.
   - **Ethernet II**: Displays source and destination MAC addresses.
   - **Internet Protocol Version 4 (IPv4)**: Shows the source and destination IP addresses, as well as the internal protocol (TCP or UDP).
   - **Transmission Control Protocol (TCP)**: Contains detailed information about TCP ports, sequence numbers, and flags.

#### Question:
What is the TCP destination port of this packet?  

![Lab8step2](https://github.com/user-attachments/assets/6ee0d675-b560-4b06-900e-4a650925fc47)

**Answer**: Port 80 is the TCP destination port, indicating HTTP traffic.

### Step 3: Using Filters to Select Packets
Use filters to analyze packets based on their source or destination addresses.

1. To filter traffic by source IP address, enter:

   `ip.src == 142.250.1.139`

![Lab8step3](https://github.com/user-attachments/assets/a76d7928-dac4-454a-82a2-e3f1ce3f2cf2)


3. To filter traffic by destination IP address, enter:

   `ip.dst == 142.250.1.139`
  
![Lab8step4](https://github.com/user-attachments/assets/88e322c7-1f35-44db-8f32-3b2787367a96)


5. To filter traffic by Ethernet MAC address, enter:

   `eth.addr == 42:01:ac:15:e0:02`

![Lab8step5](https://github.com/user-attachments/assets/051bfef4-0cb5-41c8-b62f-d1a653445b91)


7. Examine the **Ethernet II** subtree to verify that the MAC address is listed as either the source or destination address.

#### Question:
What is the protocol contained in the first packet related to MAC address `42:01:ac:15:e0:02`?  
**Answer**: TCP is the internal protocol contained in the packet.

### Step 4: Exploring DNS Packets
In this step, I filtered the DNS traffic and examined protocol data.

1. Apply the following filter to list DNS traffic:

   `udp.port == 53`

2. Double-click the first packet in the filtered list. Expand the **Domain Name System (query)** subtree to examine DNS queries.
3. For the DNS query related to `opensource.google.com`, identify the queried website and the associated IP address.


### Step 5: Exploring TCP Packets
Next, I filtered and examined TCP packets to locate specific payload data.

1. Apply the following filter to select TCP port 80 traffic:

   `tcp.port == 80`

2. Double-click the first packet in the list. Expand the **Internet Protocol Version 4** subtree to view the following details:
   - **Time to Live**: The TTL value is 64.
   - **Frame Length**: The length of the packet is 54 bytes.
   - **Header Length**: The header length is 20 bytes.
   - **Destination Address**: The destination IP address is `169.254.169.254`.

3. Use the following filter to search for specific text in packet payloads:

   `tcp contains "curl"`

This filter searches for web requests made using the `curl` command in the captured packets.

### Conclusion
Throughout this Wireshark analysis, I learned how to filter, dissect, and interpret network packets effectively. By focusing on key details such as IP addresses, protocols, DNS traffic, and specific TCP packets, I developed practical skills essential for real-world cybersecurity investigations.
