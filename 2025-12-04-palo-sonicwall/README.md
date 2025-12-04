# IOC Summary: GlobalProtect/SonicWall Credential Attack Campaign
**Campaign ID:** GNOISE-2025-GLOBALPROTECT-001  
**Report Date:** 2025-12-04  
**Severity:** HIGH  
**Source:** GreyNoise Intelligence

## Executive Summary
Multi-month credential attack campaign targeting Palo Alto GlobalProtect and SonicWall SonicOS authentication endpoints. Campaign generated 9M+ HTTP sessions between September-December 2025. Three identical client fingerprints observed across all phases despite infrastructure rotation, indicating coordinated tooling and persistent threat actor.

## Timeline
- **Sep 20 - Oct 15, 2025:** High-volume attacks from "clean" hosting ASNs (9M+ sessions)
- **Nov 20 - Nov 30, 2025:** Reduced activity, intermittent sessions
- **Dec 2, 2025:** Spike of 7000+ IPs from AS201011 targeting GlobalProtect
- **Dec 3, 2025:** SonicWall SonicOS API attacks with identical fingerprints

## Indicators of Compromise

### Autonomous Systems (ASNs)
| ASN | Organization | First Seen | Last Seen | Activity |
|-----|-------------|-----------|----------|----------|
| AS43350 | NForce Entertainment B.V. | 2025-09-20 | 2025-10-15 | GlobalProtect credential attacks |
| AS215929 | Data Campus Limited | 2025-09-20 | 2025-10-15 | GlobalProtect credential attacks |
| AS209588 | Flyservers S.A. | 2025-09-20 | 2025-10-15 | GlobalProtect credential attacks |
| AS211632 | Internet Solutions & Innovations LTD | 2025-09-20 | 2025-10-15 | GlobalProtect credential attacks |
| AS201011 | 3xK GmbH | 2025-12-02 | 2025-12-03 | GlobalProtect + SonicWall attacks (7000+ IPs) |

### Behavioral Indicators
- **Consistent client fingerprints:** Three identical fingerprints across all campaign phases
- **High session volume:** 9M+ non-spoofable HTTP sessions
- **Multi-vendor targeting:** Same tools used against Palo Alto and SonicWall
- **Infrastructure rotation:** ASN changes while maintaining tooling consistency

### Affected Products
- **Palo Alto Networks GlobalProtect** - Authentication Portal
- **SonicWall SonicOS** - API Endpoints

## Detection Rules

### GreyNoise GNQL Queries
```
classification:suspicious tags:"Palo Alto Networks GlobalProtect"
classification:suspicious tags:SonicWall
asn:AS43350 last_seen:>2025-09-01
asn:AS215929 last_seen:>2025-09-01
asn:AS209588 last_seen:>2025-09-01
asn:AS211632 last_seen:>2025-09-01
asn:AS201011 last_seen:>2025-12-01
```

### SIEM Detection Logic
**High Volume Failed Authentication - GlobalProtect**
```
event_type = "authentication_failure" 
AND product = "GlobalProtect"
AND count > 50 in 5 minutes
```

**Authentication from Campaign ASNs**
```
product IN ("GlobalProtect", "SonicOS")
AND source_asn IN (43350, 215929, 209588, 211632, 201011)
```

**Anomalous Authentication Velocity**
```
authentication_attempts > baseline * 3
AND timeframe = "1 hour"
AND product IN ("GlobalProtect", "SonicOS")
```

## Immediate Actions

### Blocking Recommendations
1. **Block traffic from identified ASNs at network perimeter**
   - AS43350, AS215929, AS209588, AS211632, AS201011
   
2. **Enable rate limiting on authentication endpoints**
   - GlobalProtect portals
   - SonicWall SonicOS API

3. **Implement GreyNoise Block** (Palo Alto/SonicWall template)
   - Filter: `classification:suspicious`
   - 14-day free trial: https://www.greynoise.io/viz/query

4. **Review authentication logs**
   - Look for velocity anomalies
   - Identify repeated failures from same sources
   - Check for successful authentications from campaign IPs

### Configuration Hardening
- Enable MFA on all VPN and API authentication endpoints
- Reduce authentication timeout windows
- Implement account lockout policies
- Enable detailed authentication logging

## Monitoring Guidance

### What to Watch For
- Authentication attempts from listed ASNs
- High-velocity login attempts (>50 in 5 minutes)
- Repeated authentication failures from single sources
- Authentication attempts using similar client fingerprints
- New ASNs exhibiting similar behavioral patterns

### Fingerprint Tracking
Monitor for the three client fingerprints consistently observed throughout this campaign. While specific fingerprint values require GreyNoise access, tracking fingerprint consistency across your authentication logs can reveal campaign persistence.

### Long-term Monitoring
- Track authentication source diversity over time
- Alert on new ASNs with high authentication volume
- Correlate failed authentications with successful ones
- Monitor for infrastructure rotation patterns

## MITRE ATT&CK Mapping
- **T1110** - Brute Force
  - **T1110.001** - Password Guessing
- **T1078** - Valid Accounts  
- **T1133** - External Remote Services

## Additional Context

### Threat Actor Assessment
- **Sophistication:** Intermediate to Advanced
- **Resources:** Significant (9M+ sessions, multiple ASNs)
- **Persistence:** Multi-month campaign with infrastructure rotation
- **Targeting:** Enterprise security infrastructure (VPN, API endpoints)

### Campaign Characteristics
- Maintains tooling consistency across infrastructure changes
- Targets multiple vendors with same tools
- High session volume indicates automated tooling
- Infrastructure rotation suggests operational security awareness

## Response Priorities
1. **CRITICAL:** Block identified ASNs immediately
2. **HIGH:** Review authentication logs for suspicious activity
3. **HIGH:** Enable MFA if not already implemented
4. **MEDIUM:** Implement fingerprint tracking
5. **MEDIUM:** Establish baseline authentication metrics
6. **LOW:** Review and update incident response procedures

## GreyNoise Resources
- **Query Console:** https://www.greynoise.io/viz/query
- **Free Trial:** 14-day trial of GreyNoise Block feature
- **GNQL Documentation:** https://docs.greynoise.io/docs/using-gnql

## Contact Information
**Report Author:** Noah Stone, Head of Content, GreyNoise Intelligence  
**Organization:** GreyNoise Intelligence  
**Report Date:** December 4, 2025

---
*This IOC package is based on GreyNoise Intelligence analysis of large-scale internet scanning and attack activity captured by their Global Observation Grid (GOG).*
