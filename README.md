# Fail2Ban Configuration for Asterisk and FreePBX

This README provides instructions for configuring **Fail2Ban** to protect your Asterisk/FreePBX server from malicious IP addresses by banning them after a set number of failed attempts.

## Table of Contents
1. [Fail2Ban Installation](#fail2ban-installation)
2. [Fail2Ban Configuration for Asterisk](#fail2ban-configuration-for-asterisk)
3. [Restart Fail2Ban](#restart-fail2ban-to-apply-changes)
4. [Checking Fail2Ban Status](#checking-fail2ban-status)
5. [Troubleshooting Fail2Ban](#troubleshooting-fail2ban)
6. [Conclusion](#conclusion)

---

## Fail2Ban Installation

**Fail2Ban** is a service that scans log files for signs of malicious activity (like brute-force login attempts) and automatically bans the offending IP addresses by adding them to the firewall rules.

### Install Fail2Ban
To install **Fail2Ban**, run the following command:

```bash
sudo apt-get update
sudo apt-get install fail2ban
````

Once installed, the service should start automatically. If it doesn't, start it manually with:

```bash
sudo systemctl start fail2ban
```

<a href="#fail2ban-configuration-for-asterisk-and-freepbx" style="text-decoration:none; display:inline-block; text-align:center;">
  <!-- Paste your entire SVG here -->
  <svg version="1.1" xmlns="http://www.w3.org/2000/svg" width="40" height="40" viewBox="0 0 512 512" >
    <path d="M0 0 C1.01790619 0.00215515 2.03581238 0.0043103 3.08456421 0.00653076 C17.69363523 0.05620146 32.02575853 0.30709809 46.375 3.3125 C47.34985352 3.51117676 48.32470703 3.70985352 49.32910156 3.91455078 C88.38660539 12.08468046 124.82400319 27.71035417 156.375 52.3125 C157.25929688 52.98539063 158.14359375 53.65828125 159.0546875 54.3515625 C174.64487101 66.4551235 189.25704477 80.75418497 201.375 96.3125 C202.52162109 97.71628906 202.52162109 97.71628906 203.69140625 99.1484375 C238.32002637 142.39252491 256.81365997 197.89189907 256.69067383 253.03979492 C256.6875221 255.97938487 256.71104926 258.9179558 256.73632812 261.85742188 C256.78098737 275.23056192 255.57551542 288.12666711 253.375 301.3125 C253.09281616 303.01805054 253.09281616 303.01805054 252.80493164 304.75805664 C245.77946967 343.86954746 228.79665906 381.05202178 204.375 412.3125 C203.61574219 413.28445313 202.85648437 414.25640625 202.07421875 415.2578125 C189.73986402 430.63741644 175.93895499 445.19015196 160.375 457.3125 C159.43914062 458.07691406 158.50328125 458.84132813 157.5390625 459.62890625 C125.58628299 485.2157721 86.41988322 501.72551276 46.375 509.3125 C45.56562988 509.47621094 44.75625977 509.63992188 43.92236328 509.80859375 C13.88110013 515.67977137 -20.7615176 514.58512909 -50.625 508.3125 C-52.14794678 507.99901611 -52.14794678 507.99901611 -53.70166016 507.67919922 C-90.84546555 499.78695344 -125.70945445 483.68345578 -155.625 460.3125 C-156.59695312 459.55324219 -157.56890625 458.79398437 -158.5703125 458.01171875 C-173.94991644 445.67736402 -188.50265196 431.87645499 -200.625 416.3125 C-201.77162109 414.90871094 -201.77162109 414.90871094 -202.94140625 413.4765625 C-228.5282721 381.52378299 -245.03801276 342.35738322 -252.625 302.3125 C-252.78871094 301.50312988 -252.95242187 300.69375977 -253.12109375 299.85986328 C-258.59069558 271.87335724 -258.46977511 238.21828161 -252.625 210.3125 C-252.42632324 209.33764648 -252.22764648 208.36279297 -252.02294922 207.35839844 C-241.93598313 159.13741149 -219.89911449 114.53770064 -185.40722656 79.14160156 C-183.63301167 77.32072238 -181.87518486 75.48496071 -180.1171875 73.6484375 C-173.01832106 66.31138736 -165.60682072 59.74213624 -157.41796875 53.64794922 C-155.58092428 52.27967127 -153.75911069 50.89264471 -151.9375 49.50390625 C-143.51077324 43.13790222 -134.81596417 37.50688619 -125.625 32.3125 C-124.99464844 31.94946777 -124.36429688 31.58643555 -123.71484375 31.21240234 C-85.96656579 9.60246645 -43.19754839 -0.16448837 0 0 Z M-130.625 65.3125 C-131.58921875 66.00601563 -132.5534375 66.69953125 -133.546875 67.4140625 C-141.2116371 73.03356425 -148.43255459 79.11113959 -155.625 85.3125 C-156.78902344 86.28896484 -156.78902344 86.28896484 -157.9765625 87.28515625 C-161.95358259 90.65564239 -165.44088282 94.20523795 -168.8046875 98.1875 C-170.02592463 99.61315021 -171.282291 101.00938685 -172.5703125 102.375 C-186.00121025 116.6484264 -196.50444974 133.0360091 -205.625 150.3125 C-206.03588867 151.0849707 -206.44677734 151.85744141 -206.87011719 152.65332031 C-223.52771971 184.44421054 -231.08353472 219.93549854 -231 255.625 C-230.99868576 257.00387894 -230.99868576 257.00387894 -230.99734497 258.41061401 C-230.92026101 283.03720556 -227.16238705 305.82140576 -219.625 329.3125 C-219.38555664 330.05999512 -219.14611328 330.80749023 -218.89941406 331.57763672 C-208.88147345 362.00222414 -191.36904215 388.25319997 -170.625 412.3125 C-169.64853516 413.47652344 -169.64853516 413.47652344 -168.65234375 414.6640625 C-165.28185761 418.64108259 -161.73226205 422.12838282 -157.75 425.4921875 C-156.32434979 426.71342463 -154.92811315 427.969791 -153.5625 429.2578125 C-139.2890736 442.68871025 -122.9014909 453.19194974 -105.625 462.3125 C-104.8525293 462.72338867 -104.08005859 463.13427734 -103.28417969 463.55761719 C-78.01967374 476.7955635 -49.0689439 485.05545125 -20.625 487.3125 C-19.40586914 487.41304688 -19.40586914 487.41304688 -18.16210938 487.515625 C44.13986549 492.29747399 104.48462676 471.72555399 151.7890625 431.26416016 C153.31842696 429.94777454 154.84674263 428.63017073 156.375 427.3125 C157.15101563 426.66152344 157.92703125 426.01054687 158.7265625 425.33984375 C162.70358259 421.96935761 166.19088282 418.41976205 169.5546875 414.4375 C170.77592463 413.01184979 172.032291 411.61561315 173.3203125 410.25 C186.75121025 395.9765736 197.25444974 379.5889909 206.375 362.3125 C206.78588867 361.5400293 207.19677734 360.76755859 207.62011719 359.97167969 C224.27771971 328.18078946 231.83353472 292.68950146 231.75 257 C231.74912384 256.08074738 231.74824768 255.16149475 231.74734497 254.21438599 C231.67026101 229.58779444 227.91238705 206.80359424 220.375 183.3125 C220.13555664 182.56500488 219.89611328 181.81750977 219.64941406 181.04736328 C209.63147345 150.62277586 192.11904215 124.37180003 171.375 100.3125 C170.72402344 99.53648438 170.07304687 98.76046875 169.40234375 97.9609375 C166.03185761 93.98391741 162.48226205 90.49661718 158.5 87.1328125 C157.07434979 85.91157537 155.67811315 84.655209 154.3125 83.3671875 C140.63729964 70.49920383 124.93364968 60.07337402 108.375 51.3125 C107.56901367 50.88485352 106.76302734 50.45720703 105.93261719 50.01660156 C79.92770188 36.443

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

   * `enabled = true`: Enables the Fail2Ban filter for Asterisk.
   * `logpath`: Points to your Asterisk log file (`/var/log/asterisk/full`).
   * `action`: Defines the action to take when an IP is banned. Here, we use `iptables-allports` to block all ports for the offending IP.
   * `maxretry`: The number of allowed failed login attempts before the IP is banned.
   * `bantime`: The duration (in seconds) for which an IP is banned.

3. **Save the file and exit**.

[Top](#fail2ban-configuration-for-asterisk-and-freepbx)

---

## Restart Fail2Ban to apply changes

After saving your changes to `/etc/fail2ban/jail.local`, restart the Fail2Ban service to load the new configuration:

```bash
sudo systemctl restart fail2ban
```

Alternatively, you can reload Fail2Ban without fully restarting the service:

```bash
sudo fail2ban-client reload
```

[Top](#fail2ban-configuration-for-asterisk-and-freepbx)

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

[Top](#fail2ban-configuration-for-asterisk-and-freepbx)

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

[Top](#fail2ban-configuration-for-asterisk-and-freepbx)

---

## Conclusion

By configuring **Fail2Ban** for Asterisk, you can effectively protect your system from unauthorized access attempts, especially brute-force attacks. Fail2Ban scans the log files for malicious activity and bans offending IPs, thus securing your server.

* **Fail2Ban** is an important layer of defense, helping to prevent brute-force attacks.
* Make sure your `jail.local` file is correctly configured and that the service is running.
* Regularly monitor the Fail2Ban logs to ensure everything is functioning as expected.

For any other issues or concerns, check the Fail2Ban logs and modify your configuration as necessary.

[Top](#fail2ban-configuration-for-asterisk-and-freepbx)

---

### Troubleshooting

* **Check for Issues**: If Fail2Ban isn't banning malicious IPs, make sure the correct log paths are set.
* **Permissions**: Ensure the log files that Fail2Ban monitors are accessible by the Fail2Ban process (permissions for `/var/log/asterisk/full`).
* **Service Restart**: If changes to `jail.local` don't seem to take effect, restart the Fail2Ban service:

  ```bash
  sudo systemctl restart fail2ban
  ```

[Top](#fail2ban-configuration-for-asterisk-and-freepbx)

---
