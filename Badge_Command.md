### Basic WiFi configuration
- https://boneskull.com/micropython-on-esp32-part-1/
```
import network

sta_if = network.WLAN(network.STA_IF)
sta_if.active(True)
sta_if.scan()                             # Scan for available access points
sta_if.connect("<AP_name>", "<password>") # Connect to an AP
sta_if.isconnected()                      # Check for successful connection
```
- my network
```
sta_if.connect("jmkim", "qaz12345")
```

### module 삭제
- https://forum.micropython.org/viewtopic.php?f=2&t=5288

```
from some import module1
from some import module2
del module1
del sys.module["module1"]

sys.modules
del sys.modules["nametag"]
unload("nametag")
```

### nametag Trial & Error
```
uos.listdir()
uos.chdir("apps/nametag")

uos.remove("__init__.py")
uos.remove("app.json")
uos.remove("tagmain.py")

run("nametag")

uos.remove("nametag.gif")
uos.remove("nametag1.gif")
uos.remove("nametag2.gif")
uos.remove("nametag.gif")
```

### [ugfx 사용법](https://github.com/IBM-Developer-Korea/developer-badge-2018-apps/tree/master/docs/ugfx)
- 한글 적응
    + micropython firmware에서는 import 안됨
    + putty에서 한글 C&P 안됨
    
```
import ugfx
ugfx.init()
ugfx.clear()

ugfx.string(10, 80, '회사명', 'NanumSquareRound_Regular16', ugfx.BLACK)
ugfx.string(10, 160, '아무개', 'NanumSquare_Bold22', ugfx.BLACK)

ugfx.string(10, 80, 'Company', 'NanumSquareRound_Regular16', ugfx.BLACK)
ugfx.string(10, 160, 'Name Name Name', 'NanumSquare_Bold22', ugfx.BLACK)


ugfx.string(10, 120, 'IBM Plex Mono Bold 24', 'IBMPlexMono_Bold24', ugfx.BLACK)
ugfx.string(10, 160, 'IBM Plex Mono Light 24', 'IBMPlexMono_Light24', ugfx.BLACK)
```

### [SHA2017-badge/Firmware](https://github.com/SHA2017-badge/Firmware)
- ESP32 firmware for the SHA2017 badge
- 
