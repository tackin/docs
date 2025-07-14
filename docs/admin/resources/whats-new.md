---
sidebar_position: 1
id: whats-new
title: "What's New"
---

# 2025 March 26

Release notes OpenCloud 2.0.0 (Production release)

- 🌲 File Native Backups with PosixFS: OpenCloud introduces PosixFS to allow for easy file native backups. As all files and metadata information is stored directly on the storage (no database needed), you can create standard file-level snapshots or copies. <br />
  Previously, files and folders were stored in a hash-based structure, making the layout unreadable for humans. With PosixFS, the full file tree is directly visible on the storage, providing transparency and confidence that all data is being backed up correctly. Admins benefit from easier maintenance, fewer moving parts, and improved fault tolerance in backup and disaster recovery scenarios. <br />
  Note: Before adding, writing, or restoring files directly into the OpenCloud storage, make sure to stop OpenCloud. Once the changes are made, start it again. This ensures that all changes are properly recognized. A future feature, currently in development, called “collaborative storage” will allow external file changes (e.g., via CLI) to be detected in real time by OpenCloud and its clients.

:::warning[Breaking Change]

No migration path – There is no programmatic migration from earlier versions (using decomposedFS) to version 2.0.0. If you need assistance, please reach out in our [Matrix channel](https://matrix.to/#/#opencloud:matrix.org) or open an issue on [GitHub](https://github.com/opencloud-eu/opencloud/issues). This helps us gauge how impactful this change is and respond accordingly.

:::

# 2025 March 18

Release notes OpenCloud 1.1.0

- 🎨 Material Design Color Roles: The custom color framework has been replaced with Material Design color roles. This change standardizes theming by using a small set of base colors to generate a consistent, accessible color palette across the UI. It lays the groundwork for improved visual coherence and better support for dark mode, accessibility, and future theming options.

# 2025 February 25

Release notes OpenCloud 1.0.0

Say hello to OpenCloud 1.0.0! A fresh take on secure file sharing & collaboration! Built as a fork of ocis, OpenCloud is all about doing things right. No unnecessary fluff, no distractions—just rock-solid data management, great user experience, secure and convenient administration and an awesome service by our support team.

We believe in keeping things simple but powerful.

## 🚀 Key Features at a Glance

- Seamless File Synchronization: Access your files across all devices.
- Secure & Flexible File Sharing: Share files with granular roles, expiration dates, and password protection.
- Spaces - Collaborative Team Folders: Ensure continuity even if team members leave.
- Real-Time Collaboration: Work on documents simultaneously with Collabora Web Office.
- Advanced Search & Organization: Use full-text search, tags, and filters for quick access.
- Unlimited Storage & Uploads: No file size restrictions.
- Privacy-First Design: Zero-Knowledge principle ensures admins can't access user content.
- Cross-Client Availability: Works on Windows, Mac, Linux, Android (soon), iOS (soon), and Web.

---

## 🔄 Cross-Device Synchronization

- Automatic Sync: Keep files up to date across all devices.
- File Manager Integration: OpenCloud appears as a native drive in your file explorer.
- Offline Access: Work without an internet connection; sync updates when back online.

---

## 🔐 Secure File & Link Sharing

### File Sharing

- Granular Access Roles: Assign users as Viewers, Editors, or Uploaders.
- One-Click Sharing: Generate share links instantly.
- Expiration Dates: Set automatic revocation of shared access.
- Transparency: Keep track of who made changes to files and when.
- Unlimited Sharing: Share with as many users or groups as needed.

### Link Sharing

- Public Links: Secure external sharing - no login or account needed.
- Enforced Password Protection: Custom rules for password strength.
- Link Expiry: Auto-disable links after a set period.
- Multiple Links per File: Unique links for different recipients; revoke links individually.
- Anonymous File Drop: Secure uploads without access to other files.
- Built-in Password Generator: Creates strong passwords automatically.

---

## 📂 Spaces - Collaborative Team Folders

- Project-Based Team Folders: Designed for teams to store, access, and manage files collectively. Files in Spaces belong to multiple users, ensuring continuity even if team members leave.
- Self-Service Admin Transfer: Easily reassign space owners and assign multiple owners for shared responsibility.
- Easy Permission Control: Manage user access based on the roles Viewers, Editors, Managers.

---

## 📝 Real-Time Collaboration – Web Office (Collabora)

- Real-Time Editing: Multiple users can work on documents at the same time.
- No File Transfers: Edit directly in the browser always on the latest version.
- No Software Installation: Works entirely online, reducing costs and complexity.

---

## 🔎 Smart Search & Organization

- Full-Text Search: Find files quickly, even in scanned documents.
- Live Search: Instant results as you type.
- Image-to-Text Recognition: Extract text from images and scanned files (OCR - Optical Character Recognition).
- Advanced Filters: Search by document type, tags, date, or storage location.

### Tags

- Flexible Organization: Categorize files beyond folder structures.
- Quick Search: Find files faster using keywords.
- Audit & Compliance: Ensure traceability of important documents.

---

## 📜 File Versioning & Recovery

- Easy Recovery: Roll back to previous file versions.
- Accidental Change Protection: Recover files in case of unintended edits.
- Deleted File Recovery: Restore files from the trash bin.

---

## ⚡ High-Performance, User-Friendly Interface

- Familiar Desktop Features:
  - Right-click context menus.
  - Drag & Drop support between web and desktop.
  - Keyboard Shortcuts: (Ctrl + C, Ctrl + X, Ctrl + V).
  - Multi-Selection: (Ctrl + Click, Shift + Click).
- Instant UI Updates: No need to refresh when a file is modified.

---

## 🛡️ Security & Compliance

### File Firewall

- Block Malicious Uploads: Prevent unwanted file types like .exe or macro files.
- Allowlist & Denylist Support: Define permitted and blocked file types.

### ICAP Antivirus Interface

- Automated Malware Scanning: Scan all uploaded files before they reach user devices.
- Early Threat Detection: Prevent infections before they spread.
- Compliance Assurance: Meets security standards for home and enterprise storage.

### Zero-Knowledge Principle

- Admin Privacy Controls: Admins manage spaces without accessing file content.
- User-Owned Data: Only designated users can access stored files.

### Access Control

- Granular Permission Management: Role-Based Access Control.

### GDPR & Accessibility Compliance

- GDPR Compliant: Fully meets EU data protection regulations.
- BITV 2.0 / WCAG 2.1 Compliance: Ensures accessible web usage for all users.

---

## 📦 Unlimited File Size

- No File Size Limits: Upload large files without restrictions.

---

## 🛠️ Web Extension System

- Extension System: Add new features and third-party integrations.
- Custom UI Adjustments: Modify the interface based on specific needs.
- Simple Installation & Management: Easily install and manage extensions.

---

## 🏗️ On-Premise

- On-Premise: Fully self-hosted deployment for maximum control.

---

## 🖼️ Built-in File Preview

- Supports Common Formats: Preview images and browser-compatible videos directly in OpenCloud.

---

## 🌐 Multi-Platform Availability

- Compatible with: Windows, Mac, Linux, Android (soon), iOS (soon), and Web.
