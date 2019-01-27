# [IBM Badge 2018 참고자료](https://ibm.ent.box.com/notes/389526223092?s=qvz8si5uu5jmsf2cgbch14d65px36oi0)

### [Badge Github / developer-badge-2018-apps] (https://github.com/IBM-Developer-Korea/developer-badge-2018-apps)

# [Espruino on ESP32](https://www.espruino.com/ESP32)

# [Get on the Good Foot with MicroPython on the ESP32, Part 1 of 2 by Christopher Hiller](https://boneskull.com/micropython-on-esp32-part-1/)

### [Firmware for ESP32 boards](https://micropython.org/download/#esp32)
- Standard firmware:
esp32-20190127-v1.10-2-g35687a87e.bin (latest)
- Tutorials : http://docs.micropython.org/en/latest/pyboard/tutorial/index.html

# [Get on the Good Foot with MicroPython, Part 2](https://hackernoon.com/get-on-the-good-foot-with-micropython-part-2-e1f2efaad50b)

### REPL
```bash
help()
```

### [WebREPL (web browser interactive prompt)](http://docs.micropython.org/en/latest/esp32/quickref.html#installing-micropython)

- setup
```
import webrepl_setup
```
- connection
```
import webrepl
webrepl.start(password='jmk')
```

gogo