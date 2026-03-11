# RemoteAdminClient (Delphi 12 Edition)

Native client-server architecture for remote system administration.

This is a native Delphi 12 implementation of a TCP-based remote administration system that can gather system information, manage processes, and execute commands on a target machine.

This project is only intended to be a base for beginners to build on top of. It is not production ready, not feature rich, not secure.

---

![](/RemoteAdminDemo.gif)

https://www.virustotal.com/gui/file/f6cfc3b7f072b1116c9bfba0897cda638e1926da60d51c3905ec01e01cd6ec47/details

![](/VT1.png)
![](/VT2.png)

## Overview

The tool establishes a persistent connection between a client process and a server interface.

If a client connects to the server:

1.  Client attempts connection to server IP/Port
2.  Client sends system info (JSON)
3.  Server displays client in ListView
4.  Server processes commands
5.  Client executes commands remotely
6.  Updates UI with results

This allows remote monitoring and control of a Windows machine via TCP sockets.

---

## Features

- Native Win32 / Win64 Delphi implementation
- Uses TIdTCPClient and TIdTCPServer (Indy components)
- Multi-threaded command processing
- JSON data exchange format
- Single instance enforcement (Mutex)
- System hardware info extraction (HWID, CPU, RAM, Disk)
- Process management (Kill, List)
- UAC Bypass capability (FodHelper)

---

## Requirements

- Delphi 12 (or compatible version with VCL)
- Windows OS
- `Server.exe` (Server GUI)
- `Client.exe` (Console Client)

---

## Example Output

**Client Console Executing Commands:**
```text
[2026-01-01 12:00:00] [INFO] Attempting connection to 127.0.0.1:9000...
[2026-01-01 12:00:00] [SUCCESS] Connected to 127.0.0.1:9000
[2026-01-01 12:00:00] [SUCCESS] System info sent.
[2026-01-01 12:00:01] [INFO] Executing FodHelper UAC Bypass...
```

**Client Console Successful Connection:**
```text
[2026-01-01 12:00:00] [INFO] Connected to 127.0.0.1:9000
[2026-01-01 12:00:00] [SUCCESS] System info written to system_info.json
```

---

## How It Works

The communication protocol is plaintext based:

| Prefix | Meaning          |
|------------|------------------|
| INFO|[SysInfoJsonData]      | Initial system info payload |
| OUT|[ExfilResponseData]     | Generic Command execution response |
| CommandName                 | Execute function of same name |

The algorithm handles connection attempts:

```text
Connected → Send INFO|JSON
Loop → Wait for command
Execute → Send OUT|Result
```

When a command is received, the client:
- Maps command string to procedure
- Executes locally on remote client machine
- Sends result back via socket

---

## Project Structure

Core components:

- `Unit1` — Main Server GUI (Client management, Command routing)
- `Client` — Console Client (TCP connection, Info gathering, Execution)
- `ShowDrives` — Form for displaying drive statistics
- `ShowProcesses` — Form for displaying process lists

---

## Intended Use

- Network programming study
- TCP protocol implementation
- System interop (Registry, Processes)
- Lab environments

This tool is intended for educational purposes and controlled environments only.

---

## Limitations

- Requires network connectivity
- Dependent on VCL/Indy components
- Not optimized for high-latency networks

---

> ⚠️ This readme (documentation) was generated with the assistance of AI.

> ⚠️ All code is human written.
