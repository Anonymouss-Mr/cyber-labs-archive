# ⚡ Ultimate Linux Administration & Security Reference

A comprehensive, production-grade Linux command reference designed for Systems Administrators, Security Researchers, DevOps Engineers, and Ethical Hackers.

---

## 🧭 System Architecture & Module Map

```
📌 ARCHITECTURE OVERVIEW:
   ├── [01] Core Streams & I/O Redirection Mechanics
   ├── [02] File System Traversal & Storage Diagnostics
   ├── [03] Permissions Matrix, Ownership & Privilege Esc.
   ├── [04] System Diagnostics & Process Management Engine
   ├── [05] Forensic Search & System Indexing Utilities
   ├── [06] Stream Editing & Advanced Text Parsing Engine
   ├── [07] Data Manipulation, Binary Extraction & Cryptography
   ├── [08] Network Sockets, SSH & File Transfer Protocols
   └── [09] APT Packaging, Repositories & Service Daemons
```

---

## 1. ⚙️ Standard Streams & I/O Redirection Engine

Linux manages process inputs and outputs using integer File Descriptors (FD).

```
 ┌──────────┐      ┌─────────────────────────┐      ┌──────────────────────┐
 │  stdin   ├─────►│  Process Engine (0)     ├─────►│  stdout (FD 1)       │
 └──────────┘      └──────────┬──────────────┘      └──────────────────────┘
                              │                     ┌──────────────────────┐
                              └────────────────────►│  stderr (FD 2)       │
                                                    └──────────────────────┘
```

| File Descriptor | Technical Stream | Functional Description |
| :---: | :--- | :--- |
| **`0`** | `stdin` | Standard Input stream (Keyboard input / Piped data stream). |
| **`1`** | `stdout` | Standard Output stream (Valid execution terminal output). |
| **`2`** | `stderr` | Standard Error stream (Diagnostic error messages & warnings). |

### 🔍 Operators & Redirection Rules

#### `>` — Truncate & Write
- **Explanation:** Overwrites existing target file contents with process `stdout`.
- **Use Case:** `echo "system_configured=true" > config.ini`

#### `>>` — Append Mode
- **Explanation:** Appends process `stdout` directly to the end of a file without overwriting.
- **Use Case:** `echo "192.168.1.50 target.local" >> /etc/hosts`

#### `2>` — Stderr Redirection
- **Explanation:** Separates standard error messages and outputs them exclusively to a targeted log file.
- **Use Case:** `find / -name "*.conf" 2> error_logs.txt`

#### `2>/dev/null` — Error Suppression
- **Explanation:** Routes `stderr` output directly to the bit-bucket null device, hiding permission errors.
- **Use Case:** `find / -type f -perm -4000 2>/dev/null`

#### `2>&1` — Stream Merging
- **Explanation:** Merges `stderr` into `stdout` stream so both can be parsed by subsequent operations.
- **Use Case:** `nc -v -z 192.168.1.1 1-100 2>&1 | grep "succeeded"`

#### `| tee` — Dual Stream Splitter
- **Explanation:** Reads from standard input and writes simultaneously to terminal standard output AND target file.
- **Use Case:** `curl -s https://example.com | tee response.html`

---

## 2. 📁 Directory Traversal & Storage Diagnostics

| Command & Syntax | Technical Explanation | Practical Portfolio Example / Use Case |
| :--- | :--- | :--- |
| `pwd` | Displays the absolute directory path of the active shell session. | `pwd` *(Verify shell environment placement)* |
| `ls -la` | Lists all files including hidden files (`.`), showing permission arrays. | `ls -la /var/log/` *(Audit hidden logs & access)* |
| `cd [path]` | Changes current working location across local or mounted filesystems. | `cd /etc/nginx/sites-available/` |
| `mkdir -p [dir]` | Creates specified directory structure, creating missing parent folders. | `mkdir -p /opt/tools/recon/scans` |
| `rm -rf [dir]` | Recursively and forcefully deletes directory contents without prompting. | `rm -rf ./tmp_build/` *(Clean build caches)* |
| `du -sh [dir]` | Aggregates and displays total disk utilization of a target directory. | `du -sh /var/log/` *(Check storage consumed by logs)* |
| `df -h` | Displays total, used, and available storage across mounted filesystems. | `df -h` *(Monitor disk partition capacities)* |

---

## 3. 🔐 Permission Architecture, Security & Privilege Management

```
  d  r w x  r - x  r - x   ──► [Type: Directory]
  │  └──┬─┘  └──┬─┘  └──┬─┘
  │     │       │       └───► Others (Read, Execute = 5)
  │     │       └───────────► Group  (Read, Execute = 5)
  │     └───────────────────► Owner  (Read, Write, Execute = 7)
```

| Octal Value | Bit Structure | Security Level & Description |
| :---: | :---: | :--- |
| **`777`** | `rwxrwxrwx` | **High Risk:** Absolute read, write, and execution rights granted to everyone. |
| **`755`** | `rwxr-xr-x` | **Executable Standard:** Owner has full control; Group/Others can only read & execute. |
| **`644`** | `rw-r--r--` | **File Standard:** Owner can read/write; Group/Others restricted to read-only. |
| **`600`** | `rw-------` | **Confidential:** Access restricted strictly to the file owner (e.g., private keys). |

### 🛠 Security Enforcement Utilities

#### `chmod` — Access Rights Manipulation
- **Explanation:** Modifies bit access permissions assigned to Owner, Group, or Others.
- **Use Case:** `chmod 600 ~/.ssh/id_rsa` *(Secure private key permissions)*

#### `umask` — Baseline Privilege Masking
- **Explanation:** Defines default access restrictions subtracted from initial creation defaults (`666` files / `777` folders).
- **Use Case:** `umask 077` *(Ensure newly generated files are readable ONLY by owner)*

#### `sudo su` — Session Privilege Escalation
- **Explanation:** Elevates active command line environment context to Administrative `root` user.
- **Use Case:** `sudo su -` *(Open fully interactive administrative terminal)*

#### `install` — Secure File Placement
- **Explanation:** Copies binaries to system directories while explicitly setting user permissions and ownership in one step.
- **Use Case:** `install -m 755 custom_script.sh /usr/local/bin/custom_tool`

---

## 4. 🔍 System Diagnostics & Process Control Engine

| Command | Functional Description | Production / Pentesting Execution |
| :--- | :--- | :--- |
| `top` / `htop` | Dynamic real-time monitoring of active processes, system threads, and CPU/RAM load. | `htop` *(Monitor real-time system resource usage)* |
| `ps aux` | Generates a static snapshot of all processes running across all system users. | `ps aux \| grep "python"` *(Find running Python daemons)* |
| `kill -9 [PID]` | Transmits an uncatchable `SIGKILL` (signal 9) to terminate a target process ID immediately. | `kill -9 4120` *(Force terminate hanging process)* |
| `whoami` | Evaluates current effective user privilege level under which commands execute. | `whoami` *(Confirm root elevation during audits)* |
| `time [cmd]` | Measures exact execution elapsed time (real, user, sys CPU time) of a command. | `time nmap -sV 192.168.1.1` *(Benchmark scan duration)* |
| `systemctl` | Interface tool to start, stop, enable, or inspect background system service daemons. | `sudo systemctl enable --now ssh` *(Enable SSH on boot)* |

---

## 5. 🔎 Deep Search & System Indexing Utilities

#### `find` — Directory Tree Traversal Engine
- **Explanation:** Recursively searches live directory trees based on attributes like size, owner, pattern, or type.
- **Use Case:** `find / -type f -name "flag.txt" 2>/dev/null`
- **Attribute Search:** `find / -user bandit7 -group bandit6 -size 33c 2>/dev/null`

#### `locate` — Database Index Lookup
- **Explanation:** Queries an updated index database (`mlocate`) for instantaneous file location results.
- **Use Case:** `locate "access.log"`

#### `sudo updatedb` — Database Re-indexing
- **Explanation:** Forces system update of internal file index database used by `locate`.
- **Use Case:** `sudo updatedb` *(Run before searching newly added files)*

#### `which` / `whereis` — Binary Path Inspection
- **Explanation:** Locates the executable file location for target terminal binaries in system PATH.
- **Use Case:** `which python3` *(Output: `/usr/bin/python3`)*

---

## 6. ✂️ Stream Editing & Advanced Text Parsing Engine

```
 RAW LOG ENTRY ──► [ cut ] ──► FIELD EXTRACTION ──► [ sort ] ──► [ uniq ] ──► CLEAN UNIQUE DATA
```

#### `grep` — Regex Pattern Matcher
- **Explanation:** Searches line-by-line for matched substrings or regular expressions.
- **Options:** `-i` (Case-insensitive), `-v` (Invert selection), `-o` (Output matched string only).
- **Use Case:** `cat access.log | grep -i -o "[a-z0-9]*.google.com" | sort -u`

#### `sed` — Stream Text Modifier
- **Explanation:** Parses text streams and performs inline replacements or structural regex transformations.
- **Use Case:** `sed 's/http:/https:/g' links.txt > secure_links.txt`

#### `cut` — Delimiter Column Splitter
- **Explanation:** Cuts out targeted byte, character, or delimited field columns from input data lines.
- **Use Case:** `cut -d " " -f 1 access.log` *(Extract IP address column from web logs)*

#### `sort` & `uniq` — Deduplication Pipeline
- **Explanation:** Re-orders text lines alphabetically/numerically and filters out duplicate consecutive entries.
- **Use Case:** `sort targets.txt | uniq -u` *(Filter and display ONLY unique, non-repeated items)*

---

## 7. 🧪 Data Manipulation, Binary Extraction & Cryptography

| Command Pattern | Technical Operation | Security & CTF Use Case Example |
| :--- | :--- | :--- |
| `strings [file]` | Extracts readable ASCII characters (minimum 4 sequences) from binary files. | `strings malicious_sample.exe \| grep -i "http"` |
| `base64 -d [file]` | Decodes standardized Base64 encoded payload strings back into raw text. | `echo "cGFzc3dvcmQ=" \| base64 -d` |
| `xxd [file]` | Converts file input into formatted hex dump (or reverses hex back to binary using `-r`). | `xxd firmware.bin \| head -n 10` |
| `tr '[A-Z]' '[a-z]'` | Replaces or translates sets of characters from standard input stream. | `cat string.txt \| tr 'A-Za-z' 'N-ZA-Mn-za-m'` *(ROT13 cipher)* |
| `tar -xf [archive]` | Extracts compressed tape archive container files to local path. | `tar -xf backup.tar.gz` *(Extract repository archives)* |

---

## 8. 🌐 Network Sockets, SSH Remote Execution & Audit Tools

```
               ┌──────────────────────────────────────────────┐
               │              Netcat (nc) Engine              │
               ├──────────────────────┬───────────────────────┤
               │   Listener Mode      │    Connect Mode       │
               │   nc -lvp 4444       │    nc 10.10.10.5 4444  │
               └──────────────────────┴───────────────────────┘
```

#### `ssh` — Encrypted Remote Shell
- **Explanation:** Connects to remote network host system through authenticated SSH tunnel.
- **Use Case:** `ssh -p 2220 bandit0@bandit.labs.overthewire.org`

#### `scp` — Secure Copy Protocol
- **Explanation:** Transfers encrypted files between local and remote server hosts via SSH stream.
- **Upload:** `scp file.txt user@192.168.1.10:/home/user/`
- **Download:** `scp user@192.168.1.10:/home/user/file.txt .`

#### `nc` (Netcat) — Network Utility Swiss-Army Knife
- **Explanation:** Reads and writes arbitrary data across TCP and UDP socket connections.
- **Listener:** `nc -lvp 4444` *(Listen for incoming connection on port 4444)*
- **Port Audit:** `nc -zv 192.168.1.10 20-80` *(Scan port range 20 to 80)*

#### `dig` & `host` — DNS Resolution Utilities
- **Explanation:** Queries Name Servers directly for specific record entries (A, NS, MX, TXT).
- **Use Case:** `dig domain.com A +short` / `dig domain.com MX`

---

## 9. 📦 APT Package Manager & Repository Classification

System package indexes are stored in `/etc/apt/sources.list`.

```
                  ┌────────────────────────────────────────┐
                  │       APT Repository Structure         │
                  ├───────────────────┬────────────────────┤
                  │   Free Software   │ Non-Free Software  │
                  ├───────────────────┼────────────────────┤
                  │ Main (Official)   │ Restricted         │
                  │ Universe (Comm.)  │ Multiverse         │
                  └───────────────────┴────────────────────┘
```

| Repository Component | Maintenance & License Architecture | Example Package Content |
| :--- | :--- | :--- |
| **`Main`** | Officially supported, free open-source software provided by distro maintainers. | `gnome-terminal`, `bash` |
| **`Restricted`** | Officially supported proprietary drivers and hardware modules. | `nvidia-driver`, `amd-driver` |
| **`Universe`** | Community-maintained free and open-source software suite. | `supertuxkart`, `tools` |
| **`Multiverse`** | Non-free packages restricted by licensing constraints and copyright law. | `ubuntu-restricted-extras` |

### 🛠 Package Operations Matrix

- **`sudo apt update`** : Fetches new package listings from `/etc/apt/sources.list`.
- **`sudo apt upgrade`** : Installs available upgrades for all active installed packages.
- **`sudo apt install [pkg]`** : Fetches and installs specified software package and dependencies.
- **`sudo apt remove [pkg]`** : Uninstalls package binary executables while keeping configuration files intact.
- **`sudo apt purge [pkg]`** : Completely removes package executables along with user configuration files.
- **`sudo apt autoremove`** : Purges orphaned dependencies no longer required by any installed package.
