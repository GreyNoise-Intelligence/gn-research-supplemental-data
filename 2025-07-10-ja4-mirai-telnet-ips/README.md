# JA4 Mirai Telnet Attack IPs - July 2025

This dataset contains IP addresses associated with a global pattern of VOIP-based Telnet attacks exhibiting a unique JA4t signature, identified during GreyNoise research into anomalous traffic patterns originating from a New Mexico utility provider.

Read the full analysis in our blog post: **A Spike in the Desert: How GreyNoise Uncovered a Global Pattern of VOIP-Based Telnet Attacks**

## Dataset Details

- **File**: `2025-07-10-ja4-mirai-telnet-ips.txt`
- **Total IPs**: ~500 unique IP addresses globally
- **Collection Date**: July 10, 2025
- **Format**: Plain text file with one IP address per line

## Key Characteristics

This dataset represents IP addresses that exhibit:
- **Unique JA4t signature**: `5840_2-4-8-1-3_1460_1` (representing 90% of traffic from affected ISPs)
- **Telnet login attempts** using weak or default credentials
- **High session volumes** consistent with botnet activity
- **Scanning behavior** aligned with known Mirai variants
- **VOIP device targeting** - many IPs linked to VOIP-capable infrastructure

## Geographic Distribution

While initially identified through a concentration of ~90 IPs from Pueblo of Laguna Utility Authority in New Mexico, the global dataset includes compromised systems from various ISPs and regions, suggesting widespread exploitation of similar VOIP infrastructure.

## Attack Patterns

The IPs in this dataset have been observed:
- Conducting Telnet brute force attacks
- Attempting generic IoT default password exploitation
- Exhibiting D-Link hardcoded Telnet attack patterns
- Demonstrating coordinated botnet behavior consistent with Mirai variants

## Technical Context

These attacks primarily target:
- VOIP-enabled devices running older Linux-based firmware
- Internet-facing systems with Telnet exposed by default
- Lightly monitored and infrequently patched edge devices
- Infrastructure potentially vulnerable to CVEs dating back to 2017

## Data Format

Each line in the text file contains a single IPv4 address:

```
137.118.82.76
192.168.1.100
10.0.0.50
...
```

## Usage

This dataset can be used for:
- Network security monitoring and blocking malicious IPs
- Threat intelligence feeds and IOC enrichment
- Academic research on Mirai botnet evolution
- VOIP infrastructure security assessment
- JA4t fingerprinting research

## Defensive Recommendations

Based on this research, organizations should:
- **Block IPs** involved in this activity
- **Audit Telnet exposure**, especially on VOIP-enabled systems
- **Rotate or disable** default credentials on edge and SOHO devices
- **Monitor** for the unique JA4t signature `5840_2-4-8-1-3_1460_1`
- Use GreyNoise to identify if infrastructure is being conscripted into botnets

## Research Notes

This investigation was initiated by GreyNoise's Lead Software Engineer Jeff Golden, who identified unusual geographic clustering of malicious IPs. The analysis utilized GreyNoise's Model Context Protocol (MCP) server with AI-powered analysis to rapidly iterate on investigation paths, combined with Censys infrastructure data and tshark packet captures for enrichment.

## Attribution

Research conducted by GreyNoise Intelligence team. Data collected through GreyNoise global sensor network and enriched with infrastructure analysis from Censys and packet capture analysis.

## Disclaimer

This data is provided for research and defensive security purposes only. Users should ensure compliance with applicable laws and regulations when using this information.

## Additional Resources

- GreyNoise Visualizer: https://viz.greynoise.io/
- Dynamic IP Blocklist (waitlist): https://info.greynoise.io/dynamic-blocklists-inquiry
- GreyNoise Research on Resurgent Vulnerabilities: https://www.greynoise.io/resources/how-resurgent-vulnerabilities-jeopardize-organizational-security