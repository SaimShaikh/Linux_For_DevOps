
# 📘 All `systemctl` Commands in Linux

`systemctl` is a command-line tool used to interact with `systemd`, which is the system and service manager on most modern Linux distributions.

---

## 🔧 Service Management

| Command | Description |
|--------|-------------|
| `systemctl start <service>` | Start a service |
| `systemctl stop <service>` | Stop a service |
| `systemctl restart <service>` | Restart a service |
| `systemctl reload <service>` | Reload config without stopping the service |
| `systemctl enable <service>` | Enable service to start on boot |
| `systemctl disable <service>` | Disable service from starting at boot |
| `systemctl status <service>` | Show the status of a service |
| `systemctl is-active <service>` | Check if a service is running |
| `systemctl is-enabled <service>` | Check if a service is enabled |
| `systemctl mask <service>` | Mask a service (cannot be started) |
| `systemctl unmask <service>` | Unmask a service |
| `systemctl reload-or-restart <service>` | Reload or restart the service |
| `systemctl try-restart <service>` | Restart only if currently running |

---

## 🖥️ System State Management

| Command | Description |
|--------|-------------|
| `systemctl reboot` | Reboot the system |
| `systemctl poweroff` | Power off the system |
| `systemctl halt` | Halt the system |
| `systemctl suspend` | Suspend (sleep) mode |
| `systemctl hibernate` | Hibernate the system |
| `systemctl hybrid-sleep` | Hybrid sleep mode (suspend + hibernate) |

---

## ⛳ Target Management

| Command | Description |
|--------|-------------|
| `systemctl isolate <target>` | Switch to another target (runlevel) |
| `systemctl get-default` | Show the current default target |
| `systemctl set-default <target>` | Set the default target |
| `systemctl list-units --type=target` | List all available targets |

**Common Targets:**
- `graphical.target` – Graphical UI
- `multi-user.target` – Multi-user (CLI)
- `rescue.target` – Rescue mode (single user)
- `emergency.target` – Minimal environment

---

## 📋 Listing and Viewing

| Command | Description |
|--------|-------------|
| `systemctl list-units` | List active units |
| `systemctl list-units --type=service` | List active services |
| `systemctl list-unit-files` | Show all unit files (enabled/disabled) |
| `systemctl show <unit>` | Display low-level properties |
| `systemctl cat <unit>` | Show unit file content |
| `systemctl list-dependencies <unit>` | Show dependencies |

---

## 🛠️ Daemon & Logs

| Command | Description |
|--------|-------------|
| `systemctl daemon-reexec` | Re-execute systemd (after upgrade) |
| `systemctl daemon-reload` | Reload systemd configs |
| `journalctl` | View all logs |
| `journalctl -u <service>` | View logs for a specific service |
| `journalctl -xe` | Show detailed error logs |

---

## 📁 Unit File Locations

- `/etc/systemd/system/` – Custom user/service unit files
- `/lib/systemd/system/` – System-installed unit files

---

> ✅ **Tip:** Use `sudo` with `systemctl` when managing system-wide services.
