# Fortinet Firewall Exposure IPs - January 2024

This dataset contains IP addresses of Fortinet FortiGate firewalls observed by GreyNoise sensors engaging in suspicious or malicious activity following a major configuration leak affecting over 15,000 devices.

Read all about it at [the blog post WIP](WIP LINK)

## Dataset Details

- **Total IPs**: 366
- **Classification Breakdown**:
  - Malicious: 35 IPs
  - Suspicious: 45 IPs
  - Unknown: 286 IPs

## Observed Behaviors

Primary malicious activities include:
- SMBv1 scanning (81 instances)
- SSH brute force attempts (23 instances)
- WannaCry variant SMB traffic (13 instances)

## Data Format

The IP list is provided in plain text format, one IP per line.

## Context

These IPs are associated with CVE-2022-40684, an authentication bypass vulnerability in Fortinet FortiGate firewalls disclosed in October 2022. All IPs in this list have been observed actively engaging with GreyNoise sensors in ways that indicate compromise or malicious intent.

## Additional Resources

For real-time analysis of these and other potentially compromised Fortinet devices, visit the GreyNoise Analysis Tab at https://viz.greynoise.io/analysis