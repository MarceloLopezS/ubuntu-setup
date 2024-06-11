# Ubuntu 24.04 First Steps After Installation

1. Open Terminal and install **nala** wrapper for _apt_ package manager: `sudo apt install nala`
2. Upgrade packages: `sudo nala upgrade`
3. Set prefered display configuration on system settings. If there are multiple monitors, execute the following command to persist display settings before login (as gdm doesn't do this automatically): `sudo cp ~/.config/monitors.xml ~gdm/.config/monitors.xml` and then make gdm the owner `sudo chown gdm:gdm ~gdm/.config/monitors.xml`. You may need to repeat this process when changing display settings and want them to persist before login to your account.
4. If you use multiple storage drives, only the one that is used for the root (`/`) will be already automatically mounted. In order to automatically mount another drive, first check the mounted drives and look for the interested one using the following command on the terminal: `sudo blkid`.

![Terminal on blkid command.](https://www.liberiangeek.net/wp-content/uploads/2024/02/image-81.png)

- Copy the UUID refering to the drive of interest.
- Open the _fstab_ file with your prefered text editor (in this case, _nano_): `sudo nano /etc/fstab`
- At the bottom of the file content, you must insert the required information for the drive to automatically mount. This data must follow the format: **\<drive-path\> \<path-to-mount-directory\> \<type\> \<options\> \<dump-value\> \<pass-value\>**
  ![fstab file](https://www.liberiangeek.net/wp-content/uploads/2024/02/image-66.png)
- Corresponding to _drive-path_, you must write the route for the drive of interest (the UUID shall be used to ensure it's the correct one). Can use this format: `UUID=uuid-example-123` or follow the same structure for the already automatically mounted drives by default.
- Corresponding to _path-to-mount-directory_, you must enter the route where the drive will mount (create one if it's not yet created). For example: `/media/user/SSD1`
- Corresponding to _type_, you must specify the drive type (e.g. `ntfs`, `ext4`, etc.)
- Corresponding to _options_, you can choose a varity of permissions or simply stick with the default values writting: `defaults`
- Corresponding to _dump-value_, you must write `1` or `0` (beeing _true_ or _false_) whether to create a backup of the file system or not.
- Correspondig to _pass-value_, your must write a number representing the priority of checking the file consistency. The root file system has a value of `1` (beeing the top priority), and numbers above that will have progressively less priority. To ignore this check, type set it to `0`.
- Finally, the formatted line should look like this: `UUID=uuid-example-123 /media/user/SSD1 ntfs defaults 0 0`
- For more information, check the original guide: [How to Mount a Drive on Ubuntu 22.04? | Liberian Geek](https://www.liberiangeek.net/2024/02/mount-drive-ubuntu-22-04/)

5. Install other required programs and packages using _nala_ instead of _apt_.

## Terminal Customization:

1. Download a [Nerd Font](https://www.nerdfonts.com/font-downloads) and, once downloaded, head up to it's folder and unzip the file: `unzip Font.zip`. Then you can remove the zip: `rm Font.zip`. And finally, move it's content to the shared fonts folder: `mv * ~/.local/share/fonts/`.
2. Once the font files are moved to the shared fonts folder, revalidate the fonts cache using the command: `fc-cache -vf`.
3. Right click on terminal and click on _Preferences_. Check the _Custom font_ checkbox and select the downloaded font.
4. Install [Starship](https://starship.rs/guide/) and follow the setup.
5. Customize promt using the **starship.toml** file for config. You can use the preset from this respository.
