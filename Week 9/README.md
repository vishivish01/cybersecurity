# Project 10 - Honeypot

Time spent: 5 hours spent in total

> Objective: Setup a honeypot and provide a working demonstration of its features.

### Overview:
In this assignment, I stood up a basic honeypot and observed its effectiveness at detecting and collecting data about an attack. A honeypot is a decoy application, server, or other networked resource that intentionally exposes insecure features which, when exploited by an attacker, will reveal information about the methods, tools, and possibly even the identity of that attacker. Successful configuration and deployment of a network-accessible honeypot server can be established by:
- Creating an attack surface that is vulnerable or exposed in some way to network-based attacks
- Having a network security feature such as an IDS (intrusion detection system) configured to detect and log such attacks
- Having at least one attack against the honeypot that can be detected or logged in a way that captures information about the attack or the attacker

### Setup
For this experiment, I utilized an open-source project called Modern Honey Network (MHN). In MHN architecture, there is a single administrator VM which is used to deploy, manage and collect information from the honeypots. These honeypots are deployed as separate VMs and can be on the same network, such as in my case. Thus to run MHN, I had to setup at least two VMs: the single Admin VM and at least one honeypot VM. When deploying the virtual machines, I also had to make sure I was able to access the machines via SSH.

To get this experiment going, I provisioned a VM on Google Cloud Platform using their Compute Engine technology - their version of infrastructure as a service (IaaS). On that machine, I installed the MHN admin application which is a Flask application that exposes an HTTP API that honeypot servers can use to:
- Download a deploy script
- Connect and register
- Send intrusion detection logs

Then I provisioned another virtual machine. This machine will be used to host the actual honeypot application. After having established SSH access to the new honeypot VM, I installed the honeypot application into the VM and wired it to connect back to the admin server.

The honeypot that I chose to deploy is called Dionaea, which is a low-interaction honeypot. These honeypots might emulate a server capable of accepting SSH connections through a combination of exposed ports and decoy responses. As a result, any attempted exploitations would quickly lead to a dead end for the attacker, perhaps revealing only an IP address and a few attempted commands to the honeypot's maintainer.

### Demonstration

- I used a network security tool called nmap to attack my honeypot. Nmap (Network Mapper) is a utility for network discovery. It uses raw IP packets in novel ways to determine what hosts are on a network. Unfortunately, this wasn't working on my honeypot. Even though my honeypot was getting thousands of attacks from external sources, it wouldn't pick up my IP address if I scanned it using my local machine. Whatever was intercepted by the honeypot is displayed in the Attacks section of the admin site where the date/time, sensor, country of origin, source IP address, destination port, protocol, and type of honeypot are listed.

- Screenshot of attacks intercepted by my honeypot:
<img src="https://imgur.com/BrqT2r9.jpg">
- I deployed one sensor which accumulated 4,458 attacks at the time of writing:
<img src="https://imgur.com/okp8l2W.jpg">
- Included in repository (session.json) is a JSON export of the data collected: number of attacks, number of malware samples, etc.

## Notes

Describe any challenges encountered while doing the work: N/A

## License

    Copyright [2018] [Viswanath Misir]

    Licensed under the Apache License, Version 2.0 (the "License");
    you may not use this file except in compliance with the License.
    You may obtain a copy of the License at

        http://www.apache.org/licenses/LICENSE-2.0

    Unless required by applicable law or agreed to in writing, software
    distributed under the License is distributed on an "AS IS" BASIS,
    WITHOUT WARRANTIES OR CONDITIONS OF ANY KIND, either express or implied.
    See the License for the specific language governing permissions and
    limitations under the License.