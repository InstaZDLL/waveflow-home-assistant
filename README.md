# WaveFlow for Home Assistant

The Home Assistant app repository for [WaveFlow Server](https://github.com/InstaZDLL/waveflow-server), a self-hosted music server with a web player and the OpenSubsonic API.

[![Add this repository to your Home Assistant](https://my.home-assistant.io/badges/supervisor_add_addon_repository.svg)](https://my.home-assistant.io/redirect/supervisor_add_addon_repository/?repository_url=https%3A%2F%2Fgithub.com%2FInstaZDLL%2Fwaveflow-home-assistant)

Or, in Home Assistant, open **Settings → Apps → App store**, choose **Repositories** in the menu, and add `https://github.com/InstaZDLL/waveflow-home-assistant`.

## Apps

| App | What it is |
| --- | --- |
| [WaveFlow Server](waveflow/) | The server, from its official multi-architecture image. Its [documentation](waveflow/DOCS.md) covers the first start. |

## How it is made

Nothing is built here. [`waveflow/config.yaml`](waveflow/config.yaml) tells the Supervisor to pull `ghcr.io/instazdll/waveflow-server` at the tag named by `version`, the same image Docker users run. A new server release reaches Home Assistant when `version` moves to it here.

The image needs nothing specific to Home Assistant: since server 2.2.2 it starts on a data folder it did not create, hands it to its own account and runs the server as that account.

## License

[AGPL-3.0-only](LICENSE), like the server.
