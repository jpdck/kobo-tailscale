# kobo-tailscale

Run [Tailscale](https://tailscale.com) on Kobo e-readers with persistence across reboots.

## Supported Devices

- Kobo Libra 2
- Kobo Libra Colour/Color
- Kobo Clara BW
- Kobo Sage

Have another device? Open a PR.

## Installation

1. Download this repo to your Kobo's onboard storage at `KOBOeReader/kobo-tailscale`
2. Connect to your Kobo via SSH or terminal
3. Navigate to your device's directory:
   ```bash
   cd /mnt/onboard/kobo-tailscale/<device>/
   ```
   where `<device>` is `libra2`, `libra-color`, `clara-bw`, or `sage`
4. Run `./install-tailscale.sh`
5. Run `tailscale up` and authenticate

By default, installs Tailscale v1.90.9. To change the version for all devices, edit the `VERSION` file at the repository root, or override it with the `TAILSCALE_VERSION` environment variable.

## Upgrading

```bash
cd /mnt/onboard/kobo-tailscale/<device>/
./upgrade-tailscale.sh [version]  # Optionally specify version, otherwise uses script default
```

Replace `<device>` with your device directory (`libra2`, `libra-color`, `clara-bw`, or `sage`).

## Uninstallation

```bash
cd /mnt/onboard/kobo-tailscale/<device>/
./uninstall-tailscale.sh
```

Replace `<device>` with your device directory (`libra2`, `libra-color`, `clara-bw`, or `sage`).

## Troubleshooting

**DNS breaks after a while?** Tailscale overwrites `/etc/resolv.conf` on systems without a DNS manager. Fix:
```bash
tailscale set --accept-dns=false
```

## How It Works

- Tailscale binaries install to `/mnt/onboard/tailscale` (persistent storage)
- udev rules trigger startup on boot and WiFi events
- Libra 2 includes pre-built TUN kernel module; other devices have it built-in
- iptables binaries from Raspbian 2017-07-05 (matches Kobo's glibc version)

## Acknowledgements

- [Dylan Staley](https://dstaley.com/posts/tailscale-on-kobo-sage) - Initial Kobo Sage implementation
- [jmacindoe](https://github.com/jmacindoe/kobo-kernel-modules) - Kernel module compilation documentation
