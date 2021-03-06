# logram [![crates.io](https://img.shields.io/crates/v/logram.svg)](https://crates.io/crates/logram)

Utility that takes logs from anywhere and sends them to Telegram. Supports log collection from files, journald and docker containers. More about available log sources see at [`docs/log_sources.md`](docs/log_sources.md).

## Usage
1. Create a Telegram bot via [@BotFather](https://t.me/BotFather)
2. Download the [latest logram release](https://github.com/mxseev/logram/releases/tag/latest)
3. Install it:
    - .deb based Linux: `sudo dpkg -i logram-...amd64.deb`
    - .rpm based Linux: `sudo rpm -i logram-...x86_64.rpm`
4. Find out the chat id with your bot (see [`docs/chat_id.md`](docs/chat_id.md))
5. Change the config (`/etc/logram.yaml` in Linux) (see [`docs/config.md`](docs/config.md))
6. Run logram: `sudo systemctl start logram`
7. ... and add it to the autostart: `sudo systemctl enable logram`

Also logram can work with `log`, see [`docs/lib.md`](docs/lib.md) for detals.

## Building
If you need to build a logram manually, do this:
1. Clone repo: `git clone git@github.com:mxseev/logram.git`
2. Choose the features you want: 
    - `bin_core` - required for all log sources
    - `ls_counter` - Counter log source
    - `ls_filesystem` - Filesystem log source
    - `ls_journald` - Journald log source
    - `ls_docker` - Docker log source
3. Build the project with these features: `cargo build --release --features=bin_core,ls_filesystem`

### Making `.deb` package
1. Install [`cargo-deb`](https://github.com/mmstick/cargo-deb)
2. Edit `package.metadata.deb.features` in `Cargo.toml`
3. Build package: `cargo deb`
4. Use `target/debian/logram_..._amd64.deb`

### Making `.rpm` package
1. Install [`cargo-generate-rpm`](https://github.com/cat-in-136/cargo-generate-rpm)
2. Build project: `cargo build --release --features=bin_core,...`
3. Strip debug symbols: `strip -s target/release/logram`
4. Build package: `cargo generate-rpm`
5. Use `target/generate-rpm/logram-...x86_64.rpm`
