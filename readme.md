An unofficial command line interface to list, upload or download Elder Scrolls Online AddOns on Bethesda.net.
ZOS asked me to keep the source private, so unless that changes, this repo will only be used for issue tracking and uploading releases.

Use --help to show all available commands and options.

It has been wrapped into a Github Action by m00nyONE: [BNET Addon Upload Github Action](https://github.com/m00nyONE/bnet-upload).

### MacOS:
You may need to run the following commands first, before the cli can be run:
```
sudo xattr -c /Path/To/ESOAddOnUploaderCli.dmg
sudo xattr -rd com.apple.quarantine /Path/To/ESOAddOnUploaderCli.dmg 
chmod +x /Path/To/ESOAddOnUploaderCli.dmg
```