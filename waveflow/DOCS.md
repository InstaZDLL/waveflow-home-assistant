# WaveFlow Server

A self-hosted music server with a web player built in, and the OpenSubsonic API that apps such as Symfonium, Feishin, DSub or Juliet already speak. This app runs the [official image](https://github.com/InstaZDLL/waveflow-server) unchanged.

## First start

1. In the app's **Configuration** tab, set **Setup token** to a value of your own, at least 16 characters. Save.
2. Start the app, then **Open web UI**. The setup screen asks for that token and creates the administrator account.
3. In the web player, go to **Settings → Administration → Libraries** and add a library at the folder where your music is, for example `/media/Music`. The first scan starts on its own.

The token is only used while no account exists. You can clear it afterwards.

## Where your music goes

The app sees Home Assistant's `media` and `share` folders, read-only, at `/media` and `/share`. Put your music in either, through Samba, the Media browser or a network storage added under **Settings → System → Storage**, and point a library at it. The server never writes to these folders.

Everything the server keeps (the database, its key, artwork, podcast episodes) lives in the app's own folder, which Home Assistant's backups include. The transcode cache is left out of backups, since it is rebuilt on demand.

## Subsonic apps

Subsonic apps sign in with a **separate password**, set under **Settings → Subsonic password** in the web player. On your own network, point the app at `http://<your Home Assistant address>:4533` with your username and that password.

## Reaching it from outside

The server speaks plain HTTP on port 4533, and Subsonic apps send their credentials with every request. Keep that port on networks you trust. To listen from outside, put a reverse proxy that terminates TLS in front of it, and set **Public URL** to its `https://` address.

## Options

Every option is optional. Each one is passed to the server as the environment variable of the same name, described in the [operations guide](https://github.com/InstaZDLL/waveflow-server/blob/main/docs/guides/operations.md).

| Option | What it does |
| --- | --- |
| `WAVEFLOW_SETUP_TOKEN` | The first-run token, at least 16 characters |
| `WAVEFLOW_PUBLIC_URL` | The `https://` address behind a reverse proxy |
| `WAVEFLOW_UPDATE_CHECK` | `ask` (default), `on` or `off`: whether the server checks for new versions |
| `WAVEFLOW_METADATA_PROVIDERS` | `lastfm`, `deezer`, `theaudiodb`, comma-separated: biographies, portraits, banners |
| `WAVEFLOW_METADATA_LASTFM_KEY` | Your Last.fm key, for `lastfm` |
| `WAVEFLOW_METADATA_THEAUDIODB_KEY` | Your TheAudioDB key, for `theaudiodb` |
| `WAVEFLOW_LYRICS_PROVIDERS` | `lrclib` fetches lyrics for files that have none |
| `WAVEFLOW_PODCASTS` | `on` turns podcasts on |

Nothing leaves the server unless one of these turns it on. The [privacy guide](https://github.com/InstaZDLL/waveflow-server/blob/main/docs/guides/privacy.md) lists every outbound request.

## Known limits

- **No sidebar panel yet.** The web player opens on port 4533 in its own tab. Showing it inside Home Assistant (ingress) needs the web player to work under a path prefix, which it does not do yet.
- **amd64 and aarch64 only**, which covers Home Assistant Green, Yellow, a Raspberry Pi 4 or 5 on a 64-bit system, and x86 machines.

## Support

Report a problem with the server at [waveflow-server issues](https://github.com/InstaZDLL/waveflow-server/issues), and one with this app at [waveflow-home-assistant issues](https://github.com/InstaZDLL/waveflow-home-assistant/issues). The app's **Log** tab shows the server's log.
