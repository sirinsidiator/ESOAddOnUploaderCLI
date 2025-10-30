An unofficial command line interface to list, upload or download Elder Scrolls Online AddOns on Bethesda.net.
ZOS asked me to keep the source private, so unless that changes, this repo will only be used for issue tracking and uploading releases.

Use `--help` to show all available commands and options.

It has been wrapped into a Github Action by m00nyONE: [BNET Addon Upload Github Action](https://github.com/m00nyONE/bnet-upload).

### Usage:

#### Authentication
Before you can use any command you need to either set the `BNET_USERNAME` and `BNET_PASSWORD` env variable, or create a credentials.json file.
All commands will implicitly log you in and out when no valid session is detected.

To store a session for use with multiple commands you can either use the `login` command or the `--session` option.
The `login` command can also be used to interactively create an encrypted credentials.json file.
```shell
ESOAddonUploaderCli login
```

After you are done, you can use `logout` to invalidate the session on the server and delete the session file. Otherwise it will expire on its own after a couple hours.
```shell
ESOAddonUploaderCli logout
```

> [!CAUTION]
> If you plan to run many commands in a row, it's highly recommended to utilize sessions instead of letting the cli implicitly log in and out for each individual command.
> If you log in and out too often in a short period of time you may get rate limited by the server, or "Vault-Tec Security" may even reset your password due to "suspicious activity".

#### Uploading an Addon:
After you have used the `login` command to create a session, or prepared the required credentials in other ways, you can upload an addon.

At the very least you need to provide a zip archive and an addon id. The id of an addon can either be retrieved with the help of the `list` command, or you can just pass in a url pointing to the addon.

If you do not specify version information the cli won't publish the release automatically and you can edit it later via the GUI. You can also specify the `--no-publish` flag to explicitly prevent an upload from being published.
```shell
ESOAddonUploaderCli upload MyAddon.zip --addon-id https://mods.bethesda.net/en/elderscrollsonline/details/12345678-1234-5678-9abc-0123456789ab/MyAddon
```
Check the `--help` for the `upload` command for all available options.

The required information can also be provided via a json file:
```json
{
    "addonId": "12345678-1234-5678-9abc-0123456789ab",
    "version": "1.0.0",
    "note": "Impressive new addon that revolutionizes everything"
}
```

```shell
ESOAddonUploaderCli upload MyAddon.zip --config config.json
```

#### Downloading an Addon
To download an addon, simply use the `download` command and pass the id or url of an addon as the first argument.
It will load the latest version and automatically pick a name for the zip file based on the addon name and version.

```shell
ESOAddonUploaderCli download https://mods.bethesda.net/en/elderscrollsonline/details/12345678-1234-5678-9abc-0123456789ab/MyAddon
```

You can specify a custom name or select a different version via options. Use `--help` for more details.

#### Listing AddOns
The `list` command shows information like the id and download stats of your own addons. It can also be used list addons by other authors with the `--all` flag or the `--author` option.
```shell
ESOAddonUploaderCli list --author sirinsidiator
```
There are various options to sort and filter the list, as well as to generate a json file for use in other applications. Use `--help` for more details.

### Troubleshooting:

#### MacOS:
You may need to run the following commands first, before the cli can be used:
```shell
sudo xattr -c /Path/To/ESOAddOnUploaderCli.dmg
sudo xattr -rd com.apple.quarantine /Path/To/ESOAddOnUploaderCli.dmg 
chmod +x /Path/To/ESOAddOnUploaderCli.dmg
```

#### Windows:
It seems that Windows Command Prompt and older versions of PowerShell do not properly support the text coloring used by the cli.
It's therefore recommended to use Windows Terminal instead.
Should that not be possible, you can also set the NO_COLOR environment variable to disable colorized output.