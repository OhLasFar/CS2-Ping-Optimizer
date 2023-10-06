# CS2 Ping Optimizer

A simple guide to optimize your ping in CS2 through Windows Registry tweaks and in-game settings adjustments.

## Windows Registry Optimization

1. Press `Win + R` and type `regedit`.
2. Navigate to: `HKEY_LOCAL_MACHINE\SYSTEM\CurrentControlSet\services\Tcpip\Parameters\Interfaces`.
3. Identify your **IPAddress** (or **DhcpIPAddress** if auto-assigned).
4. Right-click > New > DWORD (32-bit) > Name: **TcpAckFrequency** > Modify: `1` (Hexadecimal).
5. Right-click > New > DWORD (32-bit) > Name: **TCPNoDelay** > Modify: `1` (Hexadecimal).
6. Restart your PC.

## CS2 Game Settings

Append the following settings to your `autoexec.cfg`:

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

## CS2 Ping Optimizer

After applying the above tweaks, play CS2 and enjoy a potentially improved ping and reduced lag, especially when playing on distant servers.

## Disclaimer

Always be cautious when making changes to the Windows Registry. It's recommended to back up your registry before making any changes. The effectiveness of these tweaks may vary based on individual system configurations and network conditions.
