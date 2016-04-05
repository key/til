# PWM

2016/04/04

PWM=Pulse Width Moduration (パルス幅変調)

GPIOのようなON / OFF端子からLEDの調光制御したりするのに使う。
ハードウェアによっては独立したPWM回路を備えるものもある。
ソフトウェアで制御することもできる（ソフトウェアPWM）。

調光の仕組みは、短時間に点滅を繰り返すことで人間の目の錯覚を利用して明るさを調節する。

- frequency = 周期
- duty cycle = デューティサイクル = オン時間

```python
import RPi.GPIO as GPIO

channel = 24
frequency = 1000  # hz

dc = 50

p = GPIO.PWM(channel, frequency)
p.start(dc)

p.ChangeDutyCycle(100)
p.ChangeFrequency(1)

p.stop()
```

## raspberrypiにおけるPWM

RPi typeAで試した。RPi typeAが備えるハードウェアPWMは2つ。
これ以上制御するにはソフトウェアPWMが使える（[raspberry-gpio-python](https://sourceforge.net/p/raspberry-gpio-python/wiki/PWM/)とか）。

RPiの標準OSであるRaspbianはReal Time OSではないので、
ユーザランドアプリケーションは応答遅延が保証されない。
そのため、ソフトウェアでPWM制御を行うとチラツキや輝度のバラつきを起こすことがある。


## 参考

- [raspberry-gpio-python](https://sourceforge.net/p/raspberry-gpio-python/wiki/PWM/)

