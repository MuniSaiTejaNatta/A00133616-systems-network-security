# Week 6 - Risk Acceptance

- **Finding:** KRNL-5830: Reboot of system is most likely needed
- **CVSS severity estimate:** Low
- **Treatment decision:** Accept
- **Justification:** Current kernel modules remain stable; reboot scheduled before the final VM snapshot, not mid-assessment.
- **Accepted by:** Lab owner (me)
- **Review trigger:** Before the final submission snapshot

---

- **Finding:** INSE-8006: Although inetd is not running, make sure no services are enabled in /etc/inetd.conf, or remove inetd service
- **CVSS severity estimate:** Medium
- **Treatment decision:** Mitigate
- **Justification:** Port 23 (telnet) is still listening via inetd. Week 3 hardening removes this package. Isolated to the intnet segment until applied.
- **Accepted by:** Lab owner (me)
- **Review trigger:** Completion of Week 3 hardening tasks

---

- **Finding:** AUTH-9262: Install a PAM module for password strength testing like pam_cracklib or pam_passwdqc
- **CVSS severity estimate:** Low
- **Treatment decision:** Mitigate
- **Justification:** Week 2 PAM hardening (pwquality) not yet applied; sudo now requires a password, which partially offsets the gap.
- **Accepted by:** Lab owner (me)
- **Review trigger:** Completion of Week 2 hardening tasks

---

- **Finding:** HTTP-6710: Disable weak protocol in nginx configuration
- **CVSS severity estimate:** Low
- **Treatment decision:** Accept
- **Justification:** The flagged line is the unused default server block; the live 443 block already restricts to TLS 1.2/1.3 only.
- **Accepted by:** Lab owner (me)
- **Review trigger:** If the default server block is ever brought into active use

---

- **Finding:** BOOT-5122: Set a password on GRUB boot loader to prevent altering boot configuration
- **CVSS severity estimate:** Medium
- **Treatment decision:** Accept
- **Justification:** ops-01 only has console access through VirtualBox on a single managed host; physical/console access risk is limited to the assessment environment.
- **Accepted by:** Lab owner (me)
- **Review trigger:** If the VM is moved to shared or multi-user hardware

---

- **Finding:** AUTH-9286: Configure maximum and minimum password age in /etc/login.defs
- **CVSS severity estimate:** Low
- **Treatment decision:** Defer
- **Justification:** Password rotation policy has little practical benefit on a short-lived lab VM reset each term; left for completeness alongside Week 2 PAM work.
- **Accepted by:** Lab owner (me)
- **Review trigger:** Completion of Week 2 hardening tasks

---
