# goblocks4mdwm - Mi statusbar para dwm (mdwm)

Una barra simple, modular, que muestra la fecha, el volumen y el clima. Se installa con make.

![Goblocks in action](https://i.imgur.com/kH1G8tr.png)

- La barra de estado utiliza un script para mostrar el volumen (para ALSA). Se debe copiar a $PATH el archivo commandmodules/volume.
- En una ciudad distinta a Corrientes se tiene que cambiar el goblocks.json para adecuar el pronóstico de wttr.in a la ubicación actual.

### Config properties
1. **prefix(optional)**:text that will be displayed before the output of command.
2. **updateSignal**: signal that can be sent to goblocks to re-run the command and refresh output in bar. This value must be in range 34-64 inclusive.
3. **command**: functionality that will produce the text for status bar. If it starts with hash-tag goblocks will try to invoke corresponding built-in function.
If it doesn't then goblocks will run command in shell(sh) and put it's output in status bar.
4. **suffix(optional)**: Text that will be displayed after the output of command
5. **Timer**: Time period after which command is being re-run and text in status bar refreshed. s for seconds(1s), m for minutes(1m), h for hours(1h).
When set to 0 the block will only update at startup and when **updateSignal** is sent to goblocks.

### Signaling Blocks
Blocks can be updated immediately by sending the corresponding **updateSignal** to the goblocks process.
For example, `kill -35 $(pidof goblocks)` will update the block with **updateSignal** 35.
Alternatively, you can signal a block with `pkill -RTMIN+<x> goblocks` where `x` is the **updateSignal** minus 34.
So `pkill -RTMIN+1 goblocks` will update blocks with **updateSignal** 35.

> Note if multiple blocks are assigned the same **updateSignal** only the first will be updated.

## Installation
Pull this repo and run:
```
make install
```
This will build this project and generate default config file at $HOME/.config/goblocks.json. After that you can simply run it with
```
goblocks &!
```

If you want to uninstall it, just run.
```
make uninstall
```

