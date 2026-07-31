**Post-Incident Service Restoration Validation**

Post-incident validation of home Internet service restoration following a storm-related power outage using provider notifications and Debian network diagnostics.

On July 27, 2026, loud thunderstorms moved through the Milford, Ohio area while my wife and I were at home. At the time, I was working on a website and preparing for the decommissioning of my original website. The severe weather caused a power outage and an associated Spectrum Internet service interruption in our home. Spectrum reported that the interruption began at 7:39 PM, and I received the service-restoration notification at 10:37 PM.

The following morning, I conducted a structured post-incident validation from my Debian Linux workstation. In a business environment, restoring a service is only part of the recovery process. IT teams also need to verify that the fix worked, confirm that affected systems are operating normally, and identify any remaining impact before the incident can be considered resolved. I documented this real home-network event as a lab to demonstrate that same validation process on a smaller scale.

I then worked to confirm that local network connectivity, Internet access, DNS resolution, and HTTPS service access had recovered successfully. I documented my actions, evidence, findings, and conclusions in this repository.

**Objective**

- Review the provider outage and restoration notifications.
- Validate that the Debian workstation reconnected to the local network.
- Confirm that local routing, Internet connectivity, DNS resolution, and HTTPS access were working after service restoration.

**Provider Outage Notification**

- Reviewed the Spectrum outage notification received on July 27, 2026.
- Confirmed that Spectrum attributed the Internet service interruption to a local power outage.
- Recorded the reported outage start time of 7:39 PM.
- Recorded the estimated restoration time of 10:45 PM.

<img src="images/01-provider-outage-notification.png" alt="Spectrum power outage and Internet service interruption notification" width="700"/>

**Service Restoration Notification**

- Reviewed the Spectrum service restoration notification.
- Recorded that the restoration notification was received at 10:37 PM on July 27, 2026.
- Confirmed that Spectrum reported Internet service as restored.
- Noted that intermittent issues could continue while additional restoration work was completed.

<img src="images/02-provider-restoration.png" alt="Spectrum Internet service restoration notification" width="700"/>

**System and Interface Validation**

- Recorded the workstation date, time, and uptime after power and Internet service were restored.
- `9:37`: The workstation had been running for 9 hours and 37 minutes.
- `wlp0s20f3`, `wifi`, `connected`, and `UP`: The Wi-Fi adapter was enabled and connected.
- `192.168.1.x/24`: The workstation had a valid private address on the local network.
- Sanitized the username, hostname, and IPv6 addressing before publication.

- The Debian workstation was operating normally.
- The wireless connection was active.
- The system had successfully rejoined the local network.

<img src="images/03-system-interface.png" alt="Debian system uptime, wireless interface, and IP address validation" width="700"/>

**Routing and Network Connectivity Validation**

- Reviewed the routing table and tested both local and external connectivity.
- `192.168.1.1` through `wlp0s20f3`: Internet traffic was routed through the local gateway over Wi-Fi.
- `192.168.1.0/24`: The workstation was connected to the expected local network.
- `4 received, 0% packet loss`: The local gateway responded to every test packet.
- `1.1.1.1` with `4 received, 0% packet loss`: Public Internet connectivity was working.
- `time=... ms`: The response times showed how long each packet took to reach the destination and return.

- The workstation could reach the local router.
- It could also reach the public Internet without relying on DNS.
- No packet loss was detected during either test.

<img src="images/04-network-connectivity.png" alt="Default route, local gateway, and external Internet connectivity validation" width="700"/>

**DNS and HTTPS Validation**

- Used `dig` to test DNS resolution and `curl` to test HTTPS website access.
- `NOERROR` and `ANSWER: 2`: The DNS request succeeded and returned two records.
- `A`: The returned records contained public IPv4 addresses for the domain.
- The DNS request was processed through the local network gateway.
- `HTTP/2 301`: The website returned a permanent redirect.
- `location` and `server: cloudflare`: The request was redirected to the expected `www` address through Cloudflare.

- DNS resolution was working correctly.
- The website responded without an error or timeout.
- The results confirmed that public web access had recovered.

<img src="images/05-dns-https.png" alt="DNS resolution and HTTPS response validation for SunPath SEO" width="700"/>

**Skills Demonstrated**

- Linux network interface and IP address validation
- Routing table and default gateway review
- Local and external connectivity testing with `ping`
- DNS resolution testing with `dig`
- HTTPS response testing with `curl`
- Post-incident validation and technical documentation
- Evidence sanitization for public documentation

**Summary**

The checks I performed after the storm and after service was restored confirmed that my primary workstation, my Debian desktop, had reconnected to the local network and received a valid private IP address. My desktop successfully reached both the local gateway and the public Internet with no packet loss. DNS resolution and HTTPS access were also working correctly.

Instead of relying only on Spectrum’s notification that service had been restored, I performed my own validation to independently confirm that the service was operational from my Debian workstation. In a business environment, this type of post-incident validation provides hard evidence that the impacted systems are back to operating as expected. It is also part of the process of communicating the recovered state to users and stakeholders and closing the incident or support ticket with confidence.

Navigation

[`Back to GitHub Profile`](https://www.github.com/cbueker-it)

