# Networking

**Network Types :**&#x20;

* Wide Area Network (WAN)  => Internet&#x20;
* Local Area Network (LAN) => Internal Networks
* Wireless Local Area Network (WLAN) => Internal Networks accessible over Wi-Fi
* Virtual Private Network (VPN) => Connects network sites to one LAN&#x20;
  * Site-To-Site VPN  => allow multiple locations to communicate as if they were local&#x20;
  * Remote Access VPN => Virtual Interface client'side.
  * SSL VPN => Web Browser side

### **Network Topologies :**&#x20;



**Connections :**&#x20;

* Coaxial cabling => Wi-Fi
* Glass Fiber Cabling => Cellular&#x20;
* Twisted-pair Cabling => Satellite

**Type :**&#x20;

* Point-to-Point  => Direct physical Link exit only between two Hosts.

<figure><img src=".gitbook/assets/image (7).png" alt=""><figcaption><p>Point-to-Point</p></figcaption></figure>

* Bus  => No central network component . The transmission medium could be a coaxial cable. only one host can send, and all the others can only receive and evaluate the data.

<figure><img src=".gitbook/assets/image (8).png" alt=""><figcaption><p>BUS</p></figcaption></figure>

* Star => Each host is connected to the central network component via separate link (router, hub, switch)&#x20;

<figure><img src=".gitbook/assets/image (6).png" alt=""><figcaption><p>Star</p></figcaption></figure>

* Ring  => Each host is connected to the ring with two cables  ( incoming signals and outgoing ).&#x20;

<figure><img src=".gitbook/assets/image (4).png" alt=""><figcaption><p>Ring</p></figcaption></figure>

* Mesh => Decentralized networks where each node connects directly to multipe neighboring nodes, creating a redundant and resilient network structure.

<figure><img src=".gitbook/assets/image (5) (1).png" alt=""><figcaption><p>Mesh </p></figcaption></figure>

* Tree => The Central node (root) connects to multiple downstream nodes in a hierarchical manner.

<figure><img src=".gitbook/assets/image (2) (1) (1).png" alt=""><figcaption><p>Tree</p></figcaption></figure>

* Hybrid => Combine elements of different network topologies to leverage their respective advantages offering redundancy and hierarchical architecture.&#x20;

<figure><img src=".gitbook/assets/image (1) (1) (1).png" alt=""><figcaption><p>Hybrid</p></figcaption></figure>

* Daisy Chain => Each node is connect to the next one, forming a sequential network.&#x20;

<figure><img src=".gitbook/assets/image (3) (1) (1).png" alt=""><figcaption><p>Daisy Chain</p></figcaption></figure>

**Forward Proxy :**  When a client makes a requesti to a computer and that computer carriers out the request => Intermediaire.

<figure><img src=".gitbook/assets/image (2) (1).png" alt=""><figcaption><p>Forward Proxy</p></figcaption></figure>

**Reverse Proxy :** Instead of filtering outgoing request it filters incoming ones. The moast common goal with a Reverse Proxy, is to listen on an adress and forward it to a closed-off network.&#x20;

<figure><img src=".gitbook/assets/image (3) (1).png" alt=""><figcaption><p>Reverse Proxy</p></figcaption></figure>

### **Networking Models**&#x20;

**PDU =>** Protocol Data Unit&#x20;

<figure><img src=".gitbook/assets/image (3).png" alt=""><figcaption><p>OSI relations </p></figcaption></figure>

**Application :** Controls the input and output of data and provides the application functions.&#x20;

**Presentation :** Transfert the system-dependent presentation of data into a form independent of the application.&#x20;

**Session :** Controls the logical connection between two systems and prevents, for exemple, connection breakdowns or other problems.&#x20;

**Transport :** Used for end-to-end control of the transferred data. Can detect and avoid congestion situations and segment data.&#x20;

**Network :** Connections are etablished in circuit-switched networks, and data packets are forwarded in packet-switched networks. Data is transmitted over the entire network from to the receiver.&#x20;

**Data Link :** The Central task of the layer 2 is to enable reliable and error-free transmissions on the respective medium. For the purpose, the bitsreams from layer 1 are divided into blocks or frames.

**Physical :** Electrical Signals, opticals signals or electromagnetic waves. Through layer1, the transmission takes place on wired or wireless transmission lines.



### The TCP/IP Model :&#x20;

The Most important tasks of TCP/IP are :&#x20;

* **Logical Addressing  => IP**
* **Routing => IP**&#x20;
* **Error & Control Flow  => TCP**
* **Application Support  => TCP**
* **Name Resolution => DNS**

