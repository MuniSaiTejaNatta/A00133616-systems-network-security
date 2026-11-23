# Week 6 - Framework Mapping

## Framework mapping table

| Decision made | Week | CIS safeguard | NIST CSF 2.0 | ISO 27001:2022 | Evidence file |
|---|---|---|---|---|---|
| Enforced TLS 1.2/1.3 only, disabling TLS 1.0/1.1 and SSLv3 on the HTTPS server block | 5 | 4.1 | PR.DS-02 | A.8.24 | tls-confirm.png |
| Redirected all HTTP (port 80) traffic to HTTPS (port 443) via a 301 redirect | 5 | 12.2 | PR.DS-02 | A.8.20 | tls-confirm-2.png |
| Configured SSH for key-only authentication, disabling password authentication | 5 | 6.5 | PR.AA-03 | A.8.5 | ssh-key-auth.png |
| Restricted nftables to default-drop on input/forward, allowing only required ports from defined source networks | 7 | 12.2 | PR.AA-05 | A.8.20 | nftables-ruleset.png |
| Required a password for sudo (removed NOPASSWD) to enable account lockout controls | 8 | 4.1 | PR.AA-05 | A.8.2 | auth-surface-after-hardening.png |
| Configured PAM faillock to lock the account after 5 consecutive failed authentication attempts | 8 | 4.1 | PR.AA-05 | A.8.5 | auth-surface-after-hardening.png |
| Added a static ARP entry for attacker-01 to prevent spoofing of its address | 8 | 12.2 | PR.PS-01 | A.8.20 | static-arp-defense.png |
| Added a Content-Security-Policy header (default-src 'self') to the nginx HTTPS response | 8 | 4.1 | PR.PS-01 | A.8.9 | csp-before-after.png |
| Deployed WireGuard VPN and excluded SSH from the VPN subnet, limiting tunnel access to HTTPS/ICMP only | 9 | 12.6 | PR.DS-02 | A.8.24 | wg-handshake.png |

## CSF 2.0 function coverage

| CSF 2.0 function | Covered so far? | Evidence | Gap | Treatment |
|---|---|---|---|---|
| GV | No | None | No governance/policy documentation produced | Add a short policy statement in the final reflection |
| ID | Partial | nmap-full-scan.png, nmap-stealth-scan | No formal asset inventory | Single asset (ops-01); acceptable for lab scope |
| PR | Yes | TLS config, SSH keys, firewall rules, static ARP entry | Week 2/3 hardening not yet applied | Apply before final submission if time allows |
| DE | Partial | nft-drop-log.png, auth.log, faillock output | No centralised logging or alerting | Accepted; out of assessment scope |
| RS | Partial | CSP header and static ARP entry added in response to Week 8 attacks | No formal incident response procedure | Accepted; single-operator lab |
| RC | No | None | No backup/recovery procedure tested | VM snapshots serve as informal recovery |

## CIS Controls v8 IG1 status (Controls 4, 5, 6, 12)

| Safeguard | Title | IG | Status | Evidence or reason |
|---|---|---|---|---|
| 4.1 | Establish and Maintain a Secure Configuration Process | IG1 | Partial | TLS, SSH and firewall configuration documented across Weeks 5, 7, 8 |
| 4.2 | Establish and Maintain a Secure Configuration Process for Network Infrastructure | IG1 | Done | nftables-ruleset.png (Week 7) |
| 4.6 | Securely Manage Enterprise Assets and Software | IG1 | Partial | SSH hardened (Week 5); OS packages not fully patched (Lynis KRNL-5830) |
| 4.7 | Manage Default Accounts on Enterprise Assets and Software | IG1 | Not done | backup-svc still holds sudo group membership; Week 2 scoping not applied |
| 5.1 | Establish and Maintain an Inventory of Accounts | IG1 | Not done | No formal account inventory created this term |
| 5.2 | Use Unique Passwords | IG1 | Partial | Sudo now password-protected (Week 8); pwquality module not installed (Week 2 pending) |
| 5.3 | Disable Dormant Accounts | IG1 | Not done | backup-svc reviewed but not disabled |
| 5.4 | Restrict Administrator Privileges to Dedicated Administrator Accounts | IG1 | Partial | Sudo restricted to newadmin; command scoping (Week 2) not applied |
| 6.1 | Establish an Access Granting Process | IG1 | Not done | Access granted informally during lab setup |
| 6.2 | Establish an Access Revoking Process | IG1 | Not done | Not exercised this term |
| 6.3 | Require MFA for Externally-Exposed Applications | IG1 | N/A | No externally-exposed application in scope (intnet only) |
| 6.4 | Require MFA for Remote Network Access | IG1 | Not done | TOTP (Week 2) intentionally skipped; key-only SSH used instead |
| 6.5 | Require MFA for Administrative Access | IG1 | Not done | Same as 6.4 |
| 12.1 | Ensure Network Infrastructure is Up-to-Date | IG1 | Partial | Lynis flags a pending kernel update (KRNL-5830); firewall/VPN config current |
