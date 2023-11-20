
# Upgrade Netcat 🚀

![GitHub last commit](https://img.shields.io/github/last-commit/pentestfunctions/upgrade-netcat)
![GitHub issues](https://img.shields.io/github/issues/pentestfunctions/upgrade-netcat)
![GitHub](https://img.shields.io/github/license/pentestfunctions/upgrade-netcat)
![GitHub stars](https://img.shields.io/github/stars/pentestfunctions/upgrade-netcat?style=social)

This repository hosts a script that significantly enhances the functionality of a Netcat shell during penetration testing. The script upgrades a basic Netcat shell to a fully interactive TTY shell, which provides an improved interface and additional features for shell interactions.

## What It Does 🛠️

The script dynamically identifies the available Python and shell binaries on the target system. It then uses Python to upgrade the basic Netcat shell to a fully interactive TTY shell, enhancing its functionality and usability. 

### The Script Explained

- `python_bin=$(ls /bin | grep -m 1 -E '^python[0-9.]*$')`: This part of the script lists all files in `/bin`, filters for Python executables, and assigns the first match to `python_bin`. It ensures that any version of Python available on the target system is used.
- `shell_bin=$(ls /bin | grep -E '^(sh|bash)$' | head -n 1)`: This command searches for either `sh` or `bash` in `/bin` and sets `shell_bin` to the first one found. `sh` is a more universally available shell, hence prioritized.
- `$python_bin -c "import pty; pty.spawn('/bin/$shell_bin')"`: Here, the identified Python binary is used to spawn a new shell instance (`bash` or `sh`), using Python's `pty` module for pseudo-terminal handling, resulting in an interactive TTY shell.

## Usage 📖

1. **Execute the Script**: Run the command in your Netcat shell to upgrade it.
   ```bash
   python_bin=$(ls /bin | grep -m 1 -E '^python[0-9.]*$'); shell_bin=$(ls /bin | grep -E '^(sh|bash)$' | head -n 1); [ -n "$python_bin" -a -n "$shell_bin" ] && $python_bin -c "import pty; pty.spawn('/bin/$shell_bin')"
   ```

2. **Background the Shell**: Press `CTRL + Z` to put the Netcat shell in the background.

3. **Prepare Your Terminal**:
   ```bash
   stty raw -echo ; fg
   ```
   This configures your terminal to support the interactive features of the upgraded shell. Hit `Enter` twice after this command.

4. **Set Terminal Type**: 
   ```bash
   export TERM=xterm
   ```
   This sets your terminal type to `xterm`, which is widely compatible and supports advanced features.

## License 📄

Licensed under the [MIT License](LICENSE).

## Contributions 🤝

Contributions, issues, and feature requests are welcome! Visit [issues page](https://github.com/pentestfunctions/upgrade-netcat/issues).

---

Give a ⭐️ if this project helped you!
