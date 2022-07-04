# Decrypting Malicious HTTPS Traffic with Wireshark

In this exercise, I use a PCAP file containing HTTPS traffic alongside Wireshark to analyze malicious traffic. It's important to note that HTTPS traffic is HTTP secured with a TLS certificate (formerly known as SSL). The principal motivation for HTTPS is the confidentiality and integrity of data in transit, which are upheld through the usage of digital certificates.

NOTE: I am provided with the relevant TLS keys used to encrypt and decrypt HTTPS traffic. These were captured in a man-in-the-middle (MITM) attack when the malicious traffic was captured.


Here is a glimpse of of what the PCAP and TLS keys look like in this "unboxing":

![step1](https://user-images.githubusercontent.com/32144498/177210403-ffff6f0f-77cc-43f8-8ad0-f79fa2d1767c.png)

I decided to modify the UI of my Wireshark to gain a more complete picture of the traffic. Here, I add both the Source and Destination ports of each packet (Edit>Preferences>Columns).

![step2](https://user-images.githubusercontent.com/32144498/177210927-d372813a-1f3b-4a22-a888-b14a1a2e27d6.png)


The goal of this exercise is to simulate the role of the Blue Team. We have been given a PCAP file to analyze, and so the objective here is to develop a more comprehensive picture of the malicious traffic. Wireshark provides a myriad of utilities that allow an Analyst to filter through a large abundance of traffic and pinpoint the traversal of malicious traffic through a network.

Here, we can filter the traffic to view the TLS handshake. A successful handshake includes TLS version specification, an agreement on a select cipher suite, authentication of parties, and the generation of session keys.

The following filter is used to display the the successful TLS handshake:

        tls.handshake.type eq 1

![step3](https://user-images.githubusercontent.com/32144498/177214409-39743bde-f328-411d-968b-11b5c2b1ddc4.png)

To view the encrypted TCP data: right-click on a packet > Follow > TCP Stream. This encrypted data is visualized with an amalgamation of ASCII characters:

![step4](https://user-images.githubusercontent.com/32144498/177214779-fa68b509-6b96-472d-9515-be909270726b.png)

