# Phase 4 — Network Monitoring and Traffic Analysis

## 1. Objective

The objective of this phase was to practice network traffic monitoring and analysis in an authorized virtual lab using Wireshark and TShark. The exercise focused on identifying SSH traffic and recording evidence of observed network communications.

## 2. Lab Environment

- Operating system: Kali Linux
- Virtualization: VMware
- Capture interface: `eth0`
- Kali VM address: `192.168.154.128/24`
- Monitoring tools: Wireshark 4.6.6 and TShark
- Protocol investigated: SSH over TCP port 22

## 3. Procedure

1. Checked the Kali VM network interface and confirmed that `eth0` was up.
2. Verified that the SSH service was active.
3. Opened Wireshark and captured traffic on `eth0`.
4. Used a Windows PowerShell SSH client to connect to the Kali VM and authenticated in the lab.
5. Applied the Wireshark display filter `tcp.port == 22` to focus on SSH traffic.
6. Saved the capture as a PCAPNG file.
7. Used `capinfos` and TShark to inspect the capture and count packets matching TCP port 22.
8. Calculated and compared SHA-256 hashes before and after transferring the capture to Windows.

## 4. Results

| Measurement | Observed result |
|---|---|
| Capture format | PCAPNG |
| Capture interface | `eth0` |
| Total captured packets | 290,884 |
| Capture duration | Approximately 17 minutes, 42.6 seconds |
| Capture file size | 329,648,776 bytes |
| Packets matching `tcp.port == 22` | 1,158 |
| SSH server endpoint observed | `192.168.154.128:22` |
| Client endpoint observed | `192.168.154.1` |
| Client source ports observed | `52219`, `61258` |
| SHA-256 | `664b8ff476e89d9aeadf7a53ea31d72bbb2b3a1314cabbe759041922924665a7` |

The endpoint counts showed traffic in both directions for two TCP source ports. These observations are consistent with SSH communications involving the Kali VM. The packet count alone does not establish whether all matching packets belong to the intentional test connection.

## 5. Integrity Verification

The capture's SHA-256 hash was obtained in Kali and independently calculated on the Windows copy. Both values matched:

`664b8ff476e89d9aeadf7a53ea31d72bbb2b3a1314cabbe759041922924665a7`

This verifies that the transferred file matches the original file at the time of hashing.

## 6. Security Observations and Limitations

- Packet capture can reveal network endpoints, ports, timing, packet sizes, and connection patterns.
- SSH encrypts its application data after key exchange. A packet capture should not be treated as evidence that SSH passwords or session contents are readable.
- The observed traffic is not, by itself, evidence of a security attack or unauthorized access.
- The capture includes 290,884 packets and is approximately 315 MiB, so it should be retained as local lab evidence rather than committed directly to this repository.
- This exercise demonstrates basic packet capture and filtering. It does not constitute a comprehensive network security assessment.

## 7. Evidence

The full capture is retained locally at:

`Phase-4-Network-Monitoring/evidence/phase4_ssh_traffic.pcapng`

The capture was transferred from Kali to Windows and its SHA-256 hash was verified. The full capture is intentionally excluded from the Git repository because it exceeds GitHub's ordinary 100 MiB per-file limit.

## 8. Skills Practiced

- Wireshark packet capture
- TShark command-line analysis
- TCP port and endpoint filtering
- SSH traffic observation
- PCAPNG evidence handling
- SHA-256 integrity verification
- Technical documentation and evidence management
