# OpenWrt for Xiaomi Mi WiFi 3C (Mi Wifi Router 3C / R3C / R3L)

GitHub Actions workflow to build optimized, custom official OpenWrt firmware image for the Xiaomi Mi WiFi 3C.

## Build Specifications
- **Target Device:** Xiaomi Mi WiFi 3C (`ramips / mt76x8`)
- **Base Version:** OpenWrt Stable Release (`25.12.6`)
- **Included Packages:** LuCI base web interface (`luci-base`), Wi-Fi drivers & WISP support (`wpad-basic-mbedtls`, `wireless-tools`), PPPoE modules (`ppp`, `ppp-mod-pppoe`), and IPv6/DHCPv6 stack (`odhcp6c`, `odhcpd-ipv6only`).
- **Optimizations:** Strictly tuned below the 7.7 MB (`7,733,248 bytes`) safe threshold for direct flashing from OEM stock firmware, with Wi-Fi enabled by default.

---

## Initial Installation Instructions (From Stock Xiaomi Firmware)
1. **Gain Telnet Access:** Use [OpenWRTInvasion](https://github.com/acecilia/OpenWRTInvasion) to exploit and open a telnet session on your router (IP: `192.168.31.1`, User: `root`, Password: `root`).
2. **Connect via Telnet:** Open your terminal or a telnet client and connect to the router.
3. **Backup Partitions (Crucial):** Run the following command to back up your flash partitions, then transfer `/tmp/mtd0` to your computer via FTP:

   ```sh
   dd if=/dev/mtd0 of=/tmp/mtd0
   ```

4. **Upload Firmware:** Transfer the downloaded `openwrt-ramips-mt76x8-xiaomi_miwifi-3c-squashfs-sysupgrade.bin` file to the `/tmp` directory on the router using FTP.
5. **Flash OpenWrt:** Execute the following commands to install OpenWrt onto the primary OS partition:

   ```sh
   mtd erase OS1
   mtd erase OS2
   mtd -r write /tmp/openwrt-ramips-mt76x8-xiaomi_miwifi-3c-squashfs-sysupgrade.bin OS1
   ```
