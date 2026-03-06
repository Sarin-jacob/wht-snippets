# utils

## Serve Current Directory on Port 80

`http` `server` `python` Quickly spins up a web server in the current directory. Note: Port 80 usually requires sudo/administrator privileges.


---

### bash

```bash
sudo python3 -m http.server 80
```

### pwsh

```powershell
python -m http.server 80
```

## Convert Jupyter Notebook to Markdown

`jupyter` `nb2md` `converter` `uvx` Executes nb2md ephemerally via uvx to convert a notebook without polluting the global environment.


---

### bash

```bash
uvx nb2md notebook.ipynb
```

## Pretty Print YAML

`yaml` `format` `uvx` Uses rich-cli via uvx to beautifully format and colorize a YAML file in the terminal.


---

### bash

```bash
uvx --from rich-cli rich.exe data.yaml
```

## Ping Sweep /24 Subnet

`network` `ping` `scanner` Rapidly pings all 254 addresses in a subnet in parallel. Edit the base IP variable before running.


---

### bash

```bash
BASE_IP="192.168.1"; for i in {1..254}; do ping -c 1 -W 1 $BASE_IP.$i >/dev/null 2>&1 && echo "$BASE_IP.$i is UP" & done; wait
```

### pwsh

```powershell
$Base = "192.168.1"; 1..254 | ForEach-Object -Parallel { if (Test-Connection -ComputerName "$using:Base.$_" -Count 1 -Quiet -TimeoutSeconds 1) { Write-Output "$using:Base.$_ is UP" } } -ThrottleLimit 50
```

## Kill Process by Port

`port` `kill` `network` Instantly finds and force-kills whatever process is hogging a specific port (e.g., 8080).


---

### bash

```bash
kill -9 $(lsof -t -i:8080)
```

## Generate Random Password

`security` `password` `generator` `uvx` Generates a highly secure, 20-character random password using Python's secrets module directly from the shell.


---

### bash

```bash
uvx --python 3.12 python -c "import secrets, string; print(''.join(secrets.choice(string.ascii_letters + string.digits + string.punctuation) for _ in range(20)))"
```

## Extract Any Archive

`tar` `zip` `extract` A smart extraction one-liner that uses python's built-in shutil to unpack zip, tar, gztar, bztar, or xztar without needing to remember specific tar flags.


---

### bash

```bash
python3 -c "import shutil, sys; shutil.unpack_archive(sys.argv[1])" archive.zip
```