# Pedometer Home Widget for Maemo Leste

A home screen widget for Maemo Leste on the F(x)tec Pro1X: steps, distance
and calories for today and for the week, the last seven days or all time,
and a daily goal. Tapping it shows the last seven days as a bar chart.

It is a port of Andrei Mirestean's Pedometer Home Widget for Maemo 5
(pedometerhomewidget 0.3-4, GPL-3.0-or-later), with the same settings
(unit, walking or running, height class or own step length, weight) and the
same formulas for distance and calories.

The N900 widget counted the steps itself and read the accelerometer every
25 ms to do so. On the Pro1X the sensor core counts them in hardware, and
`pro1x-steps` (tools/pro1x-steps) offers the count on the system bus. The
widget only listens while it is on the visible desktop (pro1x-steps sends
at most one signal every five seconds); otherwise it reads the count when it
comes back into view and once just before midnight, so it does not wake the
phone while it is in the pocket.

## Install

Download the `.deb` from the [releases](https://github.com/smatkovi/pedometerhomewidget/releases),
install it with `dpkg -i` and add the widget on the home screen (long tap
on the desktop, "Add widget", "Pedometer"). Settings: the widget's settings
button in desktop edit mode.

It needs a hardware step counter on the system bus, `org.pro1x.Steps`
(`GetSteps()`, signal `StepsChanged`, steps since boot). On the F(x)tec
Pro1X that is `pro1x-steps` from
[pro1x-maemo-leste](https://github.com/smatkovi/pro1x-maemo-leste)
(tools/pro1x-steps), on the Qualcomm sensor core's pedometer.

Build: `dpkg-buildpackage -b -us -uc` on Leste, or `make install`. Data:
`~/.config/pedometer-home-widget/` (settings.ini, history, state).
