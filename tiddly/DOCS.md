# TiddlyWiki Add-on for Home Assistant (Hass.io)

This add-on allows you to run a standalone instance of [TiddlyWiki](https://tiddlywiki.com) within your Home Assistant (Hass.io) environment. TiddlyWiki is a unique non-linear notebook for capturing, organizing, and sharing complex information.

With this add-on, you can maintain a self-hosted personal wiki, journal, or knowledge base accessible from your local network or remotely if Home Assistant is exposed.

## 🧰 Features

- Full TiddlyWiki server (Node.js edition)
- Automatic startup with Home Assistant
- Customizable port and storage path
- Simple local backup with persistent storage
- Optional authentication layer (coming soon)

## 🔑 Set Admin Password

Before starting the add-on, you should generate a secure admin password hash and salt:

1. Open [this password hash generator](https://tiddly.packett.cool/#HashAdminPassword) in your browser.
2. Enter your desired admin password and generate the hash and salt.
3. Copy the generated values.

Then, in the add-on configuration, set:
- `admin_password_hash` to the generated hash
- `admin_password_salt` to the generated salt

Example:
```yaml
admin_password_hash: "..."
admin_password_salt: "..."
```

## 🛠️ Installation

1. Go to your Home Assistant instance.
2. Navigate to **Settings > Add-ons > Add-on Store**.
3. Click the three-dot menu and **Repositories**.
4. Add the following repository:
