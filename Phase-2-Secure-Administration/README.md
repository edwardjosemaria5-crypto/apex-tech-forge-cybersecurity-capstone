# Phase 2: Secure Administration

## 1. Overview

This phase of the APEX Tech Forge Academy cybersecurity capstone focuses on secure system administration using Kali Linux in a VMware virtual machine. Practical tasks included checking the network configuration, enabling the SSH service, verifying authenticated access, and reviewing host-based firewall rules.

## 2. Lab Environment

| Item                          | Details              |
| ----------------------------- | -------------------- |
| Operating system              | Kali Linux           |
| Virtualization platform       | VMware               |
| Linux account                 | `kali`               |
| Network interface             | `eth0`               |
| IPv4 address                  | `192.168.154.128/24` |
| Default gateway               | `192.168.154.2`      |
| Remote administration service | OpenSSH              |
| SSH port                      | TCP 22               |
| Firewall                      | UFW                  |

These are the values observed during the lab. Network addresses may change if the virtual network configuration changes.

## 3. Objectives

- Inspect the Linux account and network configuration.
- Start and enable the SSH service.
- Verify the service state and listening port.
- Test local and remote SSH authentication.
- Inspect firewall policies and permitted connections.
- Identify security improvements and document the evidence.

## 4. Initial Network Inspection

The following commands were run in Kali Linux:

```bash
whoami
ip -br addr
ip route
```

### Results

- `whoami` returned `kali`.
- `ip -br addr` showed `eth0` as `UP`, with IPv4 address `192.168.154.128/24`.
- `ip route` showed a default route through `192.168.154.2` using `eth0`.
- The connected lab network was `192.168.154.0/24`.

### Security Relevance

Network inspection helps administrators identify the host's network location, confirm interface status, and troubleshoot connectivity before configuring remote administration or testing access controls.

## 5. SSH Service Configuration

The initial service check used:

```bash
sudo systemctl status ssh --no-pager
```

Initially, the service showed `inactive (dead)` and `disabled`.

The service was started and configured to launch at boot with:

```bash
sudo systemctl enable --now ssh
```

The command completed successfully.

### Verification

```bash
sudo systemctl status ssh --no-pager
sudo ss -tlnp | grep ':22'
```

The results confirmed:

- The service state was `active (running)`.
- The service was `enabled`.
- The SSH configuration test (`sshd -t`) exited with status `0/SUCCESS`.
- SSH was listening on `0.0.0.0:22` and `[::]:22`.

### Security Relevance

SSH enables encrypted remote administration. Enabling the service at boot improves availability for authorized administration, but access should be limited to trusted sources and authentication should be configured appropriately.

## 6. Local SSH Authentication Test

The following command was run inside Kali:

```bash
ssh kali@127.0.0.1
```

The first connection displayed an ED25519 host-key authenticity prompt. The host key was accepted, and the user authenticated with the Kali account password.

Inside the SSH session, the following commands were run:

```bash
whoami
exit
```

The `whoami` command returned `kali`, and `exit` closed the SSH session.

**Result: Passed.** Local SSH authentication succeeded.

## 7. Remote SSH Test from Windows

From Windows PowerShell, the following command was executed:

```powershell
ssh kali@192.168.154.128
```

The first connection displayed an ED25519 host-key authenticity prompt. The displayed fingerprint matched the fingerprint observed during the local SSH test. The host key was accepted, and password authentication succeeded.

Inside the remote session:

```bash
whoami
exit
```

The `whoami` command returned `kali`. The SSH session then closed successfully and returned control to Windows PowerShell.

**Result: Passed.** The Windows host successfully connected to the Kali VM over the lab network and authenticated as `kali`.

### Security Relevance

This test confirms remote SSH connectivity from the Windows host to the Kali VM. The first-connection host-key check helps a user identify the server on subsequent connections. In a production environment, fingerprints should be verified through a trusted channel before accepting them.

## 8. Firewall Inspection

The firewall was inspected using:

```bash
sudo ufw status verbose
```

### Observed Results

- Status: `active`
- Logging: `on (low)`
- Default incoming policy: `deny`
- Default outgoing policy: `allow`
- Routed traffic: `disabled`
- IPv4 SSH rule: `22/tcp ALLOW IN Anywhere`
- IPv6 SSH rule: `22/tcp (v6) ALLOW IN Anywhere (v6)`

### Security Analysis

UFW was active and configured to deny incoming traffic by default unless a rule permits it. However, SSH was explicitly allowed from any source address that can reach the VM over IPv4 or IPv6.

**Recommended improvement:** Consider restricting SSH access to a trusted management host or lab subnet where practical. Confirm the VMware network design and retain a safe recovery method before changing firewall rules.

These firewall rules do not by themselves establish that the VM is exposed to the public internet. Reachability depends on the network configuration and surrounding controls.

## 9. Observed Shell Warning

During the local SSH session, Zsh displayed:

```text
zsh: corrupt history file /home/kali/.zsh_history
```

The warning did not prevent SSH authentication or use of the shell.

**Status:** Observed but not repaired. Preserve the original history file before attempting any repair.

## 10. Findings

1. The Kali VM had an active network interface and a configured default route.
2. SSH was initially stopped and disabled.
3. SSH was subsequently started and enabled at boot.
4. The SSH service passed its configuration check and listened on TCP port 22.
5. Local SSH authentication succeeded.
6. Remote SSH authentication from Windows to Kali succeeded.
7. UFW was active with a default-deny incoming policy.
8. SSH was permitted from all source addresses under the displayed IPv4 and IPv6 rules.
9. A Zsh history-file warning was observed and remains unresolved.

## 11. Evidence Checklist

Capture and save genuine terminal screenshots or other evidence for each item. Mark an item complete only after its evidence has been saved.

- [x] Initial network inspection (`whoami`, `ip -br addr`, `ip route`).
- [x] Initial SSH service state.
- [x] SSH enabled and running.
- [x] SSH listening on port 22.
- [x] Successful local SSH authentication.
- [x] Successful Windows-to-Kali SSH authentication.
- [x] UFW status, default policies, and SSH rules.

Store the evidence in this phase's evidence folder, for example `evidence/`. Do not include passwords, tokens, or other secrets in screenshots or documentation.

## 12. Recommendations

- Review whether SSH access can be restricted to trusted management sources.
- Consider SSH key-based authentication as an additional hardening measure after establishing a safe recovery method.
- Continue monitoring SSH and firewall logs during authorized lab activity.
- Investigate the Zsh history warning separately, preserving the original file before attempting repairs.
- Keep evidence and documentation consistent with the commands actually executed.

## 13. Conclusion

The completed work demonstrates practical use of Linux network-inspection commands, SSH service administration, authenticated local and remote connections, and firewall-policy review. The main connectivity objective was achieved: Windows successfully connected to the Kali VM over SSH. Potential improvements remain around restricting SSH access and investigating the shell-history warning.

## 14. Phase Status

**Core SSH administration and connectivity tests completed.** Firewall configuration was inspected, and hardening opportunities were identified. Evidence collection and the remaining capstone activities must be tracked separately.
