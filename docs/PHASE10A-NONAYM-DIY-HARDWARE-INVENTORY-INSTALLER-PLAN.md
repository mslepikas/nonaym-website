# Phase 10A — Nonaym DIY Hardware Inventory and Installer Decision Plan

Date: 2026-05-22

## Purpose

Design the Nonaym DIY installer startup script so it can inventory customer hardware and recommend the safest install path.

This is a planning phase only.

No image build.
No installer changes.
No destructive disk actions.
No Cloudflare changes.
No website deploy.

## Test hardware

Known test devices:

1. Raspberry Pi
2. Protectli 2420
3. Generic Intel machine
4. Lenovo computer #1
5. Lenovo computer #2

## Product goal

Nonaym DIY should work on common repurposed customer computers without promising universal compatibility.

The installer should help a non-technical user understand whether their hardware is a good fit.

## Installer startup menu

Proposed menu:

1. Inventory this computer
2. Check Nonaym DIY compatibility
3. Recommend install type
4. Save hardware report
5. Show manual install guidance
6. Exit

## Hardware inventory fields

The script should collect:

- hostname
- manufacturer
- model
- serial redacted or not collected by default
- CPU model
- CPU architecture
- CPU cores
- RAM size
- boot mode: UEFI or BIOS
- Secure Boot state if available
- disk count
- disk type
- disk size
- removable vs internal storage
- network adapters
- Ethernet adapters
- Wi-Fi adapters
- active network connection
- IP address redacted by default
- virtualization support
- operating environment: live USB, installed OS, recovery mode

## Privacy rule

The hardware report should avoid collecting sensitive identifiers by default.

Do not collect or save:

- full serial numbers
- public IP addresses
- private IP addresses unless user explicitly chooses advanced diagnostics
- Wi-Fi SSIDs
- passwords
- router credentials
- MAC addresses unless redacted or explicitly approved

## Installer profiles

### Profile A — Standard x86_64

Recommended for:

- Intel/AMD 64-bit computers
- at least 4 GB RAM
- SSD or HDD with enough space
- Ethernet available

Best for:

- generic Intel machine
- Lenovo computers
- repurposed desktops/laptops

### Profile B — Lightweight x86_64

Recommended for:

- older Intel/AMD 64-bit computers
- limited RAM
- slower disk
- basic DNS/privacy appliance only

### Profile C — Protectli Appliance

Recommended for:

- Protectli 2420
- fanless appliance-style install
- Ethernet-first setup
- always-on DNS role

### Profile D — Raspberry Pi ARM

Recommended for:

- Raspberry Pi hardware
- ARM64 build
- lightweight DNS/privacy appliance testing

Important:

Raspberry Pi requires a separate ARM image or install path.

### Profile E — Not Recommended

Use when:

- unsupported CPU architecture
- too little RAM
- too little disk
- no stable storage
- no usable network adapter
- failing disk indicators
- user cannot boot USB or cannot dedicate the machine

## Draft minimum requirements

### Standard x86_64

Recommended minimum:

- 64-bit Intel/AMD CPU
- 4 GB RAM preferred
- 32 GB storage minimum
- Ethernet preferred
- USB boot support
- Debian-compatible hardware

### Lightweight x86_64

Possible minimum:

- 64-bit Intel/AMD CPU
- 2 GB RAM minimum
- 16 GB storage minimum
- Ethernet strongly preferred

### Raspberry Pi ARM

Possible minimum:

- 64-bit Raspberry Pi model
- 2 GB RAM minimum
- reliable storage
- Ethernet preferred

### Protectli

Recommended:

- x86_64 CPU
- 4 GB RAM or more
- SSD storage
- Ethernet ports available

## Installer recommendation logic

The script should score hardware:

CPU architecture:
- x86_64 -> Standard or Lightweight
- aarch64/arm64 -> Raspberry Pi ARM path
- other -> Not recommended

RAM:
- 4 GB or more -> Standard
- 2 to 4 GB -> Lightweight
- under 2 GB -> Not recommended

Storage:
- 32 GB or more -> Standard
- 16 to 32 GB -> Lightweight
- under 16 GB -> Not recommended

Network:
- Ethernet present -> preferred
- Wi-Fi only -> caution
- no network -> not recommended

Boot mode:
- UEFI -> preferred
- BIOS -> supported if tested
- Secure Boot enabled -> warn that it may need to be disabled

## Customer-facing result examples

### Good result

This computer looks ready for Nonaym DIY Standard.

Recommended path:

Nonaym DIY Standard x86_64

### Caution result

This computer may work, but it is better suited for Nonaym DIY Lightweight.

Reasons:

- limited RAM
- older storage
- Wi-Fi-only connection

### Not recommended result

This computer is not recommended for Nonaym DIY.

Reasons:

- unsupported CPU architecture
- not enough memory
- no reliable network adapter

## Report output

Save a local report:

nonaym-hardware-report.txt

The report should include:

- date/time
- detected profile
- compatibility result
- hardware summary
- warnings
- recommended next step

The report should not include sensitive identifiers by default.

## Candidate commands

Linux commands likely useful:

- uname -m
- lscpu
- free -h
- lsblk
- df -h
- ip link
- lspci
- lsusb
- dmidecode, if available
- mokutil --sb-state, if available
- systemd-detect-virt
- hostnamectl

## Future implementation phases

Phase 10B:

Build the first read-only hardware inventory script.

Phase 10C:

Test the script on Raspberry Pi, Protectli 2420, generic Intel, and Lenovo machines.

Phase 10D:

Create installer recommendation logic.

Phase 10E:

Create customer-facing DIY readiness checklist for the website.

Phase 10F:

Decide Nonaym DIY minimum hardware requirements.

## Acceptance criteria

Phase 10A is complete when:

- hardware profiles are documented
- inventory fields are documented
- privacy rules are documented
- recommendation logic is drafted
- next implementation phases are clear
