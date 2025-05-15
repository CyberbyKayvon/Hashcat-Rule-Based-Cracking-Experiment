# Hashcat-Rule-Based-Cracking-Experiment

# Overview

This project explores how rule-based attacks in Hashcat can significantly improve the chances of cracking passwords compared to raw dictionary attacks. The experiment focuses on cracking a WPA2 password (`CyberProud2025`) using a modified rockyou wordlist and custom rule set.

## Objective
- Crack a known WPA2 hash using rule-based attacks
- Observe effectiveness of rules vs. plain dictionary
- Learn rule syntax, optimization, and performance impact

## Tools
- **Hashcat v6.x**
- **rockyou.txt** (truncated version for speed)
- **Custom Rule File** (cyberproud_rules.rule)

## Hash Example
```plaintext
$hashcat -m 2500 WPA2-HASH.hccapx wordlists/rockyou_short.txt -r rules/cyberproud_rules.rule

$1$2$3     # Add digits at the end
c          # Capitalize first letter
^C         # Insert 'C' at beginning
$2025      # Append '2025' to the end


---

### Sample `cyberproud_rules.rule`

```txt
c        # Capitalize first letter
$1       # Append '1'
$2025    # Append '2025'
^Cyber   # Prefix 'Cyber'
^C       # Insert 'C' at beginning
$!       # Add '!' at end

## Machine
- ThinkPad T14s
- CPU Only (i7 11th Gen)
- 32 GB RAM

## Observation
- Plain rockyou_short.txt: No crack after 2 hours
- With `cyberproud_rules.rule`: Cracked in under 45 min
- CPU temp stabilized at 82°C

## Script for Easy Execution

#!/bin/bash
hashcat -m 2500 hashes/test_hashes.txt wordlists/rockyou_short.txt -r rules/cyberproud_rules.rule --force
