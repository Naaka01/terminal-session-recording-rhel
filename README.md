# Configure Terminal Session Recording

Lab by **Justesse Louboulat Milandou** — Second year Cybersecurity (IIBS Dakar)

## Why this lab?

Implementing a terminal session recording lab is essential to validate the
traceability and compliance of privileged access before any production
deployment. This lab tests the raw capture of administrator activity
(screen input/output), making any history tampering or circumvention via
`sudo` impossible to conceal — a key requirement of security standards like
PCI-DSS or ISO 27001. This experimental phase also measures the real
technical impact of the solution: log centralization toward `journald`,
anticipated storage space, and absence of user-side latency, avoiding any
disruption to critical infrastructure.

## Prerequisites

- Red Hat Enterprise Linux system
- `cockpit-session-recording` and `tlog` installed

**Role of the packages:**
- `cockpit-session-recording`: visual/graphical module for the Cockpit web interface
- `tlog`: background capture and recording tool for terminal input/output flow

## What this lab covers

1. Installing `cockpit-session-recording` (pulls in `tlog` as a dependency)
2. Configuring session recording scope to `all` via SSSD (`/etc/sssd/conf.d/sssd-session-recording.conf`)
3. Fine-tuning capture parameters (notice, latency, logging) in `/etc/tlog/tlog-rec-session.conf`
4. Verifying the on-login warning banner ("ATTENTION! Your session is being recorded!")
5. Performing sample terminal actions to generate recording data
6. Replaying a user's session as video through the Cockpit web interface
7. Inspecting the raw `tlog` JSON payload stored in `journald` via `journalctl`

## Key takeaway — advantages & trade-offs

Terminal Session Recording offers absolute and tamper-proof traceability of
administrator activity by capturing all screen inputs and outputs, ensuring
compliance with strict security standards (PCI-DSS, ISO 27001) and
simplifying post-mortem analysis with minimal CPU overhead. On the flip
side, this solution generates a significant volume of logs in `journald`
that are unreadable in their raw state (JSON saturated with ANSI codes),
requires a robust audit infrastructure, and introduces a data leakage risk
if sensitive data or passwords are displayed in clear text on the screen.

## Conclusion

Implementing Terminal Session Recording in a lab environment confirms that
it is an essential pillar for modern infrastructure governance. Although
this solution introduces real technical challenges — most notably rigorous
storage volume management and the protection of sensitive data displayed
on-screen — its security benefits far outweigh them. By guaranteeing
tamper-proof traceability against privilege escalation and natively meeting
PCI-DSS or ISO 27001 compliance requirements, this tool does more than just
monitor: it enforces access accountability and sustainably secures
production.

## Sources

- https://zero.rhdp.net/lab/zt-rhelbu.zt-session-recording-tlog.prod
- https://docs.redhat.com/en/documentation/red_hat_enterprise_linux/8/html/recording_sessions/getting-started-with-session-recording_getting-started-with-session-recording
