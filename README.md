# companion-module-clockotron

A [Bitfocus Companion](https://bitfocus.io/companion) module for [Clockotron](https://github.com/dlamon1/clockotron), the countdown timer that writes into vMix text inputs.

Requires Companion 5.x and Clockotron 1.1.0. Clockotron itself needs no changes.

## Install

1. Download the latest `clockotron-x.y.z.tgz` from [Releases](https://github.com/graysonbarton-arch/companion-module-clockotron/releases).
2. In Companion, open **Modules**, click **Import module package**, and pick the file. Don't unzip it.
3. Under **Connections**, add **Clockotron**. If Companion runs on the same PC as Clockotron, the defaults (`127.0.0.1`, port `5491`) work as is.
4. Optional, recommended: turn on **Read clock from vMix** and enter the vMix input and text field that Clockotron writes to. This makes the live time, running state and time-remaining colors work.

Full setup, actions, variables and feedbacks are in [companion/HELP.md](companion/HELP.md).

## Features

- **Actions:** start/pause, reset, set time (`05:00`, `1:30:00`, `90`, `1h 5m`, variables allowed), add/subtract hours/minutes/seconds, clock speed, and Clockotron's keypad
- **Variables:** live time (`$(clockotron:time_hms)` and parts), running, connected, keypad preview
- **Feedbacks:** connected, running, and time remaining at or below a threshold
- **Presets:** 38 ready-made buttons, including a clock display that turns amber at 1:00 and red at 0

## How it works

Clockotron runs an HTTP control API on port **5491** with plain GET requests: `/start`, `/stop`, `/reset`, `/slower`, `/normal`, `/faster`, `/digit?value=N`, `/clear`, `/postClock`, and `/{h,m,s}{Up,Down}`. That API can't be read from, so the live time comes from vMix's XML API (`http://<vmix>:8088/api`). The module reads the text input that Clockotron writes to.

## Troubleshooting

- **Not connecting:** on the Clockotron PC, open `http://127.0.0.1:5491/api` in a browser. It should show `api`. If it doesn't, Clockotron's API isn't running.
- **Companion on another PC:** allow TCP port 5491 into the Clockotron PC in Windows Firewall.

## Development

```sh
npm install
npm test                       # unit tests
npx companion-module-build     # writes clockotron-<version>.tgz
```

Pushing a `v*` tag builds the package and publishes a GitHub release with the `.tgz` attached.

## License

MIT
