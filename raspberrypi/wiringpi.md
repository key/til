# WiringPi2

2016/04/05

RaspberryPi GPIO制御ライブラリ。ライセンスはLGPL。ハードウェアPWMが使えるっぽい（[RPi.GPIO](https://pypi.python.org/pypi/RPi.GPIO)はソフトウェア制御のみ？）。


```python
import wiringpi

# physical header pin number
wiringpi.wiringPiSetupPhys()

# 2=hardware pwm
wiringpi.pinMode(12, 2)

# duty 100%=1024
wiringpi.pwmWrite(12, 1024)
```
