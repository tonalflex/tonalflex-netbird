# tonalflex-netbird

Installing Netbird VPN on the embedded device running ElkOS will allow you to SSH into it from remote networks in order to develop OS-related features without physical access to the device.

## Setup on VPN server device

When you are prompted for password in any of below steps, the default password in ElkOS is `elk`.

### 1. SSH into the RPi:

```sh
ssh mind@elk-pi.local
```

### 2. Download & decompress Netbird:

_Check and update these to latest version!_

```sh
# Fetch latest release
wget https://github.com/netbirdio/netbird/releases/download/v0.40.1/netbird_0.40.1_linux_arm64.tar.gz

# Uncompress it
tar -xzf netbird_0.40.1_linux_arm64.tar.gz
```

### 3. Move Netbird into filesystem

```sh
sudo mkdir -p /usr/local/bin
sudo mv /home/mind/netbird /usr/local/bin/
```

_and confirm it's available..._

```sh
which netbird
netbird version
```

### 5. Install & Start Netbird deamon

```sh
sudo netbird service install
sudo netbird service start
```

### 4. Create Netbird Key

- Go to: [https://app.netbird.io](https://app.netbird.io) and log in.

- In the left sidebar, click **"Setup Keys"**.

- Click the **`+ Create Setup Key`** button (usually in the top-right).

- In the popup form:

  - **Name**: e.g., `tonalflex-pi`
  - **Make this key reusable**: ✅ Enable this so if you need access from multiple devices.
  - **Usage limit**: _(Optional)_ – e.g., `1` if it's a one-time setup
  - **Expiration**: _(Optional)_ – leave empty for no expiry

- Click **Create**.

- Copy the setup key that appears – it will look like: `c3d98e7d-XXXX-XXXX-XXXX-123456abcdef`

### 5. Run Netbird VPN

```sh
sudo netbird up --setup-key <your-setup-key>
```

_and confirm it's running..._

```sh
netbird status
```

## Setup on VPN client device

### 1. Install Netbird client

Download the app from [Netbird Website](https://app.netbird.io/install).

### 2. SSH into the device

Open a terminal and type:

```sh
ssh mind@elk-pi.netbird.cloud
```

_Default password: `elk`_
