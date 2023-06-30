# WiFi Profile QR Code Generator

This code generates a QR code for a WiFi network profile using the `wifi_qrcode_generator` module. It retrieves the WiFi network name (SSID) and password from the Windows operating system using the `subprocess` module.

## Prerequisites

Before running this code, make sure you have the following requirements:

- Python 3.x installed
- `wifi_qrcode_generator` module installed (can be installed using pip: `pip install wifi_qrcode_generator`)

## Usage

1. Import the required modules:
```python
import subprocess
import wifi_qrcode_generator
```

2. Run the code inside a try-except block:
```python
try:
    # Retrieve the WiFi profile
    Id = subprocess.check_output(['netsh', 'wlan', 'show', 'interfaces']).decode('utf-8').split('\n')
    id_results = str([b.split(":")[1][1:-1] for b in Id if "Profile" in b])[2:-3]

    # Retrieve the WiFi password
    password = subprocess.check_output(['netsh', 'wlan', 'show', 'profiles', id_results, 'key=clear']).decode('utf-8').split('\n')
    pass_results = str([b.split(":")[1][1:-1] for b in password if "Key Content" in b])[2:-2]

    print("User name:", id_results)
    print("Password:", pass_results)

except:
    print("Something went wrong")
```

3. Generate the QR code using the retrieved WiFi profile and password:
```python
wifi_qrcode_generator.wifi_qrcode(id_results, False, 'WPA', pass_results)
```

## Note

- This code is specifically designed for Windows operating system.
- Make sure you have administrative privileges to access the WiFi network profiles and passwords.

Feel free to customize the code or integrate it into your project as needed.
