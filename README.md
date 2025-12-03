# kobo-tailscale

Run [Tailscale](https://tailscale.com) on Kobo e-readers with persistence across reboots.

## Supported Devices

- Kobo Libra 2
- Kobo Libra Colour/Color
- Kobo Clara BW

Have another device? Open a PR.

## Installation

1. Download this repo to your Kobo's onboard storage `KOBOeReader/` into a folder named `tailscale`
2. Navigate to your device's directory (`libra2/`, `libra-color/`, or `clara-bw/`)
3. Run `./install-tailscale.sh`
4. Run `tailscale up` and authenticate

By default, installs Tailscale v1.90.9. Change version by editing `TAILSCALE_VERSION` in `install-tailscale.sh` before running.

## Upgrading

```bash
cd /mnt/onboard/tailscale/
./upgrade-tailscale.sh [version]  # Optionally specify version, otherwise uses script default
```

## Uninstallation

```bash
cd /mnt/onboard/tailscale/
./uninstall-tailscale.sh
```

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
