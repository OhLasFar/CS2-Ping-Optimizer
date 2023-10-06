# CS2 Ping Optimizer 🚀

A simple guide to optimize your ping in CS2 through Windows Registry tweaks and in-game settings adjustments.

## Windows Registry Optimization 🖥️

1. Press `Win + R` and type `regedit`.
2. Navigate to: `HKEY_LOCAL_MACHINE\SYSTEM\CurrentControlSet\services\Tcpip\Parameters\Interfaces`.
3. To identify your local IP address:
   - Press `Win + R`, type `cmd`, and press Enter.
   - In the command prompt, type `ipconfig` and press Enter.
   - Look for the "IPv4 Address" (or "IP Address" on some systems). It's usually the first one listed. This is your local IP.
4. In the Registry Editor, identify your **IPAddress** (or **DhcpIPAddress** if auto-assigned) that matches the IP you found in the previous step.
5. Right-click > New > DWORD (32-bit) > Name: **TcpAckFrequency** > Modify: `1` (Hexadecimal).
6. Right-click > New > DWORD (32-bit) > Name: **TCPNoDelay** > Modify: `1` (Hexadecimal).
7. Restart your PC.

## CS2 Game Settings 🎮

Append the following settings to your `autoexec.cfg`:

If you're unsure where to find the `autoexec.cfg` file, note that by default, this file might not exist and you'll need to create it manually. Here's how:

1. Navigate to the following path: `C:\Program Files (x86)\Steam\steamapps\common\Counter-Strike Global Offensive\csgo\cfg`
2. Check if `autoexec.cfg` is present. If not, create a new text file and name it `autoexec.cfg`.
3. Open `autoexec.cfg` and paste the provided commands/settings.

```plaintext
// NETWORK SETTINGS
rate 1000000
cl_predictweapons 1
cl_lagcompensation 1
net_client_steamdatagram_enable_override 1
net_maxroutable 1200
mm_session_search_qos_timeout 20
mm_dedicated_search_maxping 50
mm_csgo_community_search_players_min 3
cl_resend 0.5
cl_timeout 30
lobby_default_privacy_bits2 0
ui_setting_advertiseforhire_auto 1
cl_join_advertise 2
cl_invites_only_friends 0
cl_invites_only_mainmenu 0
```
5. After saving the file, right-click on `autoexec.cfg`, select **Properties**, check the **Read-only** option, and then click **OK**.
6. To ensure the game uses the settings from the `autoexec.cfg` file when launched, follow these steps to add it to the Steam launch options:
   - Open Steam and navigate to your game library.
   - Right-click on `Counter-Strike 2` and select `Properties`.
   - In the `General` tab, scroll down to the `Launch Options` section and enter `+exec autoexec.cfg`.
   - Close the properties window.
7. You're all set! You can now launch CS2, and the game will utilize the settings from the `autoexec.cfg` file.

## CS2 Ping Optimizer 📉

After applying the above tweaks, play CS2 and enjoy a potentially improved ping and reduced lag, especially when playing on distant servers.

## Disclaimer ⚠️

Always be cautious when making changes to the Windows Registry. It's recommended to back up your registry before making any changes. The effectiveness of these tweaks may vary based on individual system configurations and network conditions.

## Explanation of CS2-Ping-Optimizer Tweaks 📚

### 1. Windows Registry Tweaks:
   - **TcpAckFrequency**: This setting controls the frequency of acknowledgments sent for received TCP packets. By default, Windows might delay the acknowledgment briefly to see if it can be bundled with outgoing data. Setting this to `1` ensures that Windows acknowledges packets immediately.
   - **TCPNoDelay**: Essentially, this toggles the Nagle's algorithm. When enabled (set to `1`), it ensures that data packets are sent as soon as possible without grouping.

Both of these tweaks aim to reduce latency by ensuring that packets are sent and acknowledged without any delay.

### 2. In-game settings:
## CS2 Network Settings Explained

The provided settings adjust various network-related parameters in the game. For instance:

1. **rate 1000000**: Controls the maximum amount of data (in bytes) that the server can send to the client per second. A higher value can improve connection quality, especially on faster internet connections.
2. **cl_predictweapons 1**: Enables weapon prediction on the client side, making gameplay feel smoother.
3. **cl_lagcompensation 1**: Enables lag compensation, improving player actions' responsiveness in online games.
4. **net_client_steamdatagram_enable_override 1**: Forces the use of Steam's Datagram Relay service for a more stable connection.
5. **net_maxroutable 1200**: Sets the maximum size of packets sent from the client to the server.
6. **mm_session_search_qos_timeout 20**: Relates to matchmaking and sets a timeout for Quality of Service when searching for a game session.
7. **mm_dedicated_search_maxping 50**: Sets the maximum ping for dedicated servers in matchmaking.
8. **mm_csgo_community_search_players_min 3**: Sets the minimum number of players for community server searches.
9. **cl_resend 0.5**: Determines the time before the client resends a packet to the server.
10. **cl_timeout 30**: Sets the time before a client disconnects due to no server response.
11. **lobby_default_privacy_bits2 0**: Sets default privacy settings for game lobbies.
12. **ui_setting_advertiseforhire_auto 1**: Related to the "Looking to Play" feature in CS2.
13. **cl_join_advertise 2**: Allows friends to join your game.
14. **cl_invites_only_friends 0**: Determines who can send you game invites.
15. **cl_invites_only_mainmenu 0**: Determines when you can receive game invites.

### Effectiveness of the Tweaks:
The tweaks are legitimate methods that some users employ to potentially reduce latency in various online games. However, their effectiveness can vary based on individual system configurations, network conditions, and the specific game in question.

While these tweaks do alter how your system and game manage network traffic, the actual improvement in ping or gameplay might differ among users. It's essential to approach such guides with caution. While they might benefit some users, the results might not be as pronounced for everyone. Additionally, always remember to back up the Windows Registry before making any changes due to the inherent risks associated with modifying it.

In summary, the guide provides legitimate tweaks, but the actual benefits can vary. It's not necessarily "false advertisement," but results may differ based on individual circumstances.

---

### Connect with Me! 🌐

If you found these tweaks helpful, consider giving a follow:

- 🐦 **Twitter**: [@ohlasfar](https://twitter.com/ohlasfar)
- 🎥 **Streaming**: I stream on [kick.com/LasFar](https://kick.com/LasFar) every Tuesday at 8:15 PM EST.

Feel free to drop by during a stream or tweet at me to share your experience with the tweaks! Your feedback is appreciated. 😊

---

