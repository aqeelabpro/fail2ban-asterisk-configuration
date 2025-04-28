# Fail2Ban Configuration for Asterisk and FreePBX

This README provides instructions for configuring **Fail2Ban** to protect your Asterisk/FreePBX server from malicious IP addresses by banning them after a set number of failed attempts.

## Table of Contents
1. [Fail2Ban Installation](#fail2ban-installation)
2. [Fail2Ban Configuration for Asterisk](#fail2ban-configuration-for-asterisk)
3. [Checking Fail2Ban Status](#checking-fail2ban-status)
4. [Troubleshooting Fail2Ban](#troubleshooting-fail2ban)
5. [Conclusion](#conclusion)

---

## Fail2Ban Installation

**Fail2Ban** is a service that scans log files for signs of malicious activity (like brute-force login attempts) and automatically bans the offending IP addresses by adding them to the firewall rules.

### Install Fail2Ban
To install **Fail2Ban**, run the following command:

```bash
sudo apt-get update
sudo apt-get install fail2ban
```

Once installed, the service should start automatically. If it doesn't, start it manually with:

```bash
sudo systemctl start fail2ban
```

---

## Fail2Ban Configuration for Asterisk

### 1. Configure Fail2Ban for Asterisk

1. **Create or Edit `jail.local`**:
   
   The default configuration for Fail2Ban is stored in `/etc/fail2ban/jail.conf`. However, it’s recommended to modify the `jail.local` file to ensure your custom changes persist through Fail2Ban updates.

   Open `/etc/fail2ban/jail.local`:

   ```bash
   sudo nano /etc/fail2ban/jail.local
   ```

2. **Add the Asterisk Jail Configuration**:

   Add the following configuration to protect your Asterisk service. Make sure to customize the `logpath` if needed:

   ```ini
   [DEFAULT]
   # Add other trusted IP addresses or subnets here, use comma or space like `ip1 ip2` or `ip1,ip2`
   ignoreip = ip1 ip2

   [asterisk]
   enabled = true
   logpath = /var/log/asterisk/full
   action = iptables-allports[name=ASTERISK, protocol=all]
   maxretry = 5
   bantime = 60
   ```

   - `enabled = true`: Enables the Fail2Ban filter for Asterisk.
   - `logpath`: Points to your Asterisk log file (`/var/log/asterisk/full`).
   - `action`: Defines the action to take when an IP is banned. Here, we use `iptables-allports` to block all ports for the offending IP.
   - `maxretry`: The number of allowed failed login attempts before the IP is banned.
   - `bantime`: The duration (in seconds) for which an IP is banned.

3. **Save the file and exit**.

---

## Checking Fail2Ban Status

After configuring Fail2Ban, you should check its status to ensure it is properly protecting your Asterisk server.

### 1. Check Fail2Ban Status for Asterisk

To check the status of the Asterisk jail, run the following command:

```bash
sudo fail2ban-client status asterisk
```

This will show whether Fail2Ban is monitoring your Asterisk logs and how many IPs have been banned.

### 2. Check the Fail2Ban Service Status

If you encounter any issues, check the status of the Fail2Ban service:

```bash
sudo systemctl status fail2ban
```

If the service is not running, start it with:

```bash
sudo systemctl start fail2ban
```

---

## Troubleshooting Fail2Ban

### 1. Fail2Ban Not Starting

If Fail2Ban is not starting, check the logs for errors:

```bash
sudo tail -f /var/log/fail2ban.log
```

### 2. Check Fail2Ban Ban List

If you want to check which IP addresses have been banned by Fail2Ban, use:

```bash
sudo fail2ban-client status asterisk
```

### 3. Unban an IP Address

To unban an IP address manually, use the following command:

```bash
sudo fail2ban-client set asterisk unbanip <IP_ADDRESS>
```

Replace `<IP_ADDRESS>` with the IP you wish to unban.

---

## Conclusion

By configuring **Fail2Ban** for Asterisk, you can effectively protect your system from unauthorized access attempts, especially brute-force attacks. Fail2Ban scans the log files for malicious activity and bans offending IPs, thus securing your server.

- **Fail2Ban** is an important layer of defense, helping to prevent brute-force attacks.
- Make sure your `jail.local` file is correctly configured and that the service is running.
- Regularly monitor the Fail2Ban logs to ensure everything is functioning as expected.

For any other issues or concerns, check the Fail2Ban logs and modify your configuration as necessary.

---

### Troubleshooting

- **Check for Issues**: If Fail2Ban isn't banning malicious IPs, make sure the correct log paths are set.
- **Permissions**: Ensure the log files that Fail2Ban monitors are accessible by the Fail2Ban process (permissions for `/var/log/asterisk/full`).
- **Service Restart**: If changes to `jail.local` don't seem to take effect, restart the Fail2Ban service:

  ```bash
  sudo systemctl restart fail2ban
  ```

---
