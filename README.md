# CS2 Ping Optimizer 🚀

A precise, public-friendly guide to help you test lower-latency settings in CS2 through Windows Registry tweaks and in-game adjustments by @OhLasFar on Twitter.

## Disclaimer ⚠️

- Run `regedit` as an administrator and export every key you edit (`File > Export`) so you can revert instantly.
- Registry tweaks can produce different results depending on your NIC, router and ISP. Test before/after with tools such as `ping`, `tracert`, or in-game net graph instead of assuming instant gains.
- Some changes (like disabling TCP auto-tuning) have system-wide effects. Read each note and only apply what matches your setup.

---

## Windows Registry Optimization 🖥️

**Before you start:** Reboot first, close Steam/CS2, then follow the steps in order. Creating a System Restore point is a good safety net.

1. **Access the Registry Editor**
   - Press `Win + R`, type `regedit`, press **Ctrl + Shift + Enter** to open it with admin rights.

2. **Modify TCP settings per network interface**
   - Navigate to `HKEY_LOCAL_MACHINE\SYSTEM\CurrentControlSet\Services\Tcpip\Parameters\Interfaces`.
   - In an elevated Command Prompt run `ipconfig` and match your active adapter's `IPv4 Address` with the `IPAddress` or `DhcpIPAddress` you see under each GUID.
   - Inside the matching key, create/modify the following DWORDs:
     - `TcpAckFrequency` = `1` (Hex). Forces immediate ACKs.
     - `TCPNoDelay` = `1` (Hex). Disables Nagle's algorithm.
     - `TcpWindowSize` = `65535` (Decimal). **Only takes effect if you first disable Windows auto-tuning** by running `netsh int tcp set global autotuninglevel=disabled` in an elevated PowerShell. To revert later, run the same command with `normal`.

3. **Set NonBestEffortLimit (QoS reservation)**
   - Path: `HKEY_LOCAL_MACHINE\SOFTWARE\Policies\Microsoft\Windows`. If `Psched` does not exist, right-click `Windows > New > Key > Psched`.
   - Create `NonBestEffortLimit` (DWORD) and set it to `0` (Hex). This only affects systems where the "Limit reservable bandwidth" Group Policy is enabled, but setting it pre-emptively keeps games from being throttled if that policy ever turns on.

4. **Disable network throttling for multimedia workloads**
   - Navigate to `HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Windows NT\CurrentVersion\Multimedia\SystemProfile`.
   - Set `NetworkThrottlingIndex` to `FFFFFFFF` (Hex) and create `SystemResponsiveness` with a value of `0` (Decimal) if it does not exist. These two entries work together to give high-priority threads more network time.

5. **Apply and verify**
   - Restart Windows to load the new values.
   - After reboot, confirm your settings with `reg query` or by rerunning `netsh int tcp show global` to check the auto-tuning status.

## CS2 Game Settings 🎮

### Find or create `autoexec.cfg`

1. Open Steam > Settings > Storage and note which drive contains Counter-Strike 2.
2. Browse to `<YourSteamLibrary>\steamapps\common\Counter-Strike Global Offensive\game\csgo\cfg` (the folder name still references CS:GO).
3. If `autoexec.cfg` does not exist, create a UTF-8 text file with that name.

### Core network tuning block

```plaintext
// CORE NETWORK SETTINGS
rate 1000000                        // Allow up to 1 MB/s from the server
cl_predictweapons 1                 // Keep weapon prediction client-side
cl_lagcompensation 1                // Let the server reconcile shots
net_client_steamdatagram_enable_override 1  // Force SDR; set to 0 if SDR POPs are far away
net_maxroutable 1200                // Limit packet size to reduce fragmentation
mm_session_search_qos_timeout 20    // Wait 20s before giving up on QoS
mm_dedicated_search_maxping 25      // Refuse servers above 25 ms (raise if queues take too long)
mm_csgo_community_search_players_min 3  // Require 3+ players in community search
cl_resend 0.5                       // Retry unacknowledged packets after 0.5 s
cl_timeout 30                       // Disconnect if no server response for 30 s
```

### Optional quality-of-life block

```plaintext
// OPTIONAL SOCIAL SETTINGS
lobby_default_privacy_bits2 0
ui_setting_advertiseforhire_auto 1
cl_join_advertise 2
cl_invites_only_friends 0
cl_invites_only_mainmenu 0
```

### Make CS2 read the file every launch

4. Save the file, right-click it, open **Properties**, set it to **Read-only** so the game cannot overwrite it.
5. In Steam Library, right-click Counter-Strike 2 > **Properties** > **Launch Options** and add `+exec autoexec.cfg`.
6. Launch CS2, open the console and type `exec autoexec` once to confirm it runs without errors.

---

## Explanation of CS2-Ping-Optimizer Tweaks 📚

### 1. Windows Registry tweaks 🔧
- **TcpAckFrequency / TCPNoDelay**: Remove Windows' small batching delays so acknowledgments and small packets leave immediately. This can shave a couple milliseconds off interactions with distant servers but may slightly increase CPU usage on very slow CPUs.
- **TcpWindowSize**: Provides a fixed receive window for older games. Only meaningful when TCP auto-tuning is disabled; otherwise Windows ignores the manual value.
- **NonBestEffortLimit**: Sets the QoS reserved bandwidth ceiling to 0%, ensuring that background Group Policies cannot silently reserve 20% of your throughput.
- **NetworkThrottlingIndex + SystemResponsiveness**: Stops Windows Multimedia Scheduler from capping network throughput for foreground games/streams. Always reboot after changing these keys.

### 2. In-game settings 🔧
- **rate 1000000**: Lets high-tick servers send you more data per second, reducing choke on fast connections.
- **net_client_steamdatagram_enable_override**: `1` forces Steam Datagram Relay (SDR). Use `0` and test again if your closest SDR point of presence is far away; whichever value yields lower `loss`/`var` wins.
- **mm_dedicated_search_maxping 25**: Keeps the matchmaker from putting you on slow servers. Adjust upward (35/50) if you routinely sit in queue.
- **cl_resend / cl_timeout**: Lower resend interval and reasonable timeout tighten how quickly your client reacts to packet loss.
- **Social settings block**: Does not affect latency, but it keeps your lobby open to friends and advertises when you are looking for a party.

---

## Effectiveness & Testing 📉

Latency improvements depend on ISP routing, distance to Valve's servers, Wi-Fi vs. Ethernet, and background traffic. Record your ping/variance before and after each tweak so you can roll back anything that hurts stability. To undo registry edits, import the backups you exported earlier or delete the added values and reboot.

---

### Connect with Me! 🌐

- 🐦 **Twitter**: [@ohlasfar](https://twitter.com/ohlasfar)
- 🌐 **Dispattern**: [dispattern.com](https://dispattern.com) — Your #1 skin database for everything pattern-related and analysis in Counter-Strike 2.

---


