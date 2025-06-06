#### Q: Why is the Defold editor super small when run on a 4k or HiDPI monitor when using GNOME?

A: Change the scaling factor before running Defold. [source](https://unix.stackexchange.com/a/552411)

```bash
$ gsettings set org.gnome.desktop.interface scaling-factor 2
$ ./Defold
```

A: An alternative solution, especially when you wish to scale up by a fraction, is to modify the `Defold/config` file and on the `vmargs` line add `glass.gtk.uiScale`: [source](https://forum.defold.com/t/4k-hidpi-monitor-support-solved/64108/12?u=britzl)

```
vmargs = -Dglass.gtk.uiScale=1.5,-Dfile.encoding=UTF-8,...
vmargs = -Dglass.gtk.uiScale=175%,-Dfile.encoding=UTF-8,...
vmargs = -Dglass.gtk.uiScale=192dpi,-Dfile.encoding=UTF-8,...
```

More on this value in the [Arch Linux HiDPI wiki article](https://wiki.archlinux.org/title/HiDPI#JavaFX).

#### Q: Why does mouse clicks on Elementary OS go through the editor onto whatever is below?

A: Start the editor like this:

```bash
$ GTK_CSD=0 ./Defold
```


#### Q: The Defold editor crashes when opening a collection or game object and the crash refers to `com.jogamp.opengl`

A: On certain distributions (like Ubuntu 18) there is an issue with the version of `jogamp`/`jogl` Defold uses vs. the version of [Mesa](https://docs.mesa3d.org/) on the system. You can override which GL version that gets reported when calling `glGetString(GL_VERSION)` by setting the `MESA_GL_VERSION_OVERRIDE` to 2.1 or a larger value but less than or equal to the version of your driver. You can check which is the maximum OpenGL version your driver supports using `glxinfo`:

```bash
glxinfo | grep version
```

Example output (look for "OpenGL version string: x.y"):

```
server glx version string: 1.4
client glx version string: 1.4
GLX version: 1.4
Max core profile version: 4.6
Max compat profile version: 4.6
Max GLES1 profile version: 1.1
Max GLES[23] profile version: 3.2
OpenGL core profile version string: 4.6 (Core Profile) Mesa 20.2.6
OpenGL core profile shading language version string: 4.60
OpenGL version string: 4.6 (Compatibility Profile) Mesa 20.2.6
OpenGL shading language version string: 4.60
OpenGL ES profile version string: OpenGL ES 3.2 Mesa 20.2.6
OpenGL ES profile shading language version string: OpenGL ES GLSL ES 3.20
GL_EXT_shader_implicit_conversions, GL_EXT_shader_integer_mix,
```

Use version 2.1 or version matching your graphics driver:

```bash
$ MESA_GL_VERSION_OVERRIDE=2.1 ./Defold
```

```bash
$ MESA_GL_VERSION_OVERRIDE=4.6 ./Defold
```


#### Q: Why am I getting "`com.jogamp.opengl.GLException: Graphics configuration failed`" when launching Defold?

A: On certain distributions (for instance Ubuntu 20.04) there is an issue with the new [Mesa](https://docs.mesa3d.org/) drivers (Iris) when running Defold. You can try using an older driver version when running Defold:

```bash
$ MESA_LOADER_DRIVER_OVERRIDE=i965 ./Defold
```


#### Q: The Defold editor crashes when opening a collection or game object and the crash refers to `libffi.so`

A: The [libffi](https://sourceware.org/libffi/) version of your distribution and the one required by Defold (version 6 or 7) does not match. Make sure `libffi.so.6` or `libffi.so.7` is installed under `/usr/lib/x86_64-linux-gnu`. You can download `libffi.so.7` like this:  

```bash
$ wget http://ftp.br.debian.org/debian/pool/main/libf/libffi/libffi7_3.3-6_amd64.deb
$ sudo dpkg -i libffi7_3.3-6_amd64.deb
```

Next you specify the path to this version in the `LD_PRELOAD` environment variable when running Defold:

```bash
$ LD_PRELOAD=/usr/lib/x86_64-linux-gnu/libffi.so.7 ./Defold
```


#### Q: My OpenGL drivers are outdated. Can I still use Defold?

A: Yes, it might be possible to use Defold if you enable software rendering. You can enable software rendering by setting the `LIBGL_ALWAYS_SOFTWARE` environment variable to 1:

```bash
$ LIBGL_ALWAYS_SOFTWARE=1 ./Defold
```


#### Q: Why doesn't my Defold game start when I try to run it on Linux?

A: Check the console output in the editor. If you get the following message:

```
dmengine: error while loading shared libraries: libopenal.so.1: cannot open shared object file: No such file or directory
```

Then you need to install *`libopenal1`*. The package name varies between distributions, and in some cases you might have to install the *`openal`* and *`openal-dev`* or *`openal-devel`* packages.

```bash
$ apt-get install libopenal-dev
```

#### Q: Why does the top menu close before I can select something?

A: This is likely caused by the window manager used (for instance `Qtile` or i3). This is a [known issue in JavaFX](https://bugs.openjdk.org/browse/JDK-8251240?focusedCommentId=14362084&page=com.atlassian.jira.plugin.system.issuetabpanels%3Acomment-tabpanel#comment-14362084) and it can either be solved by setting the `GDK_DISPLAY` environment variable to 1:¨

```bash
$ GDK_DISPLAY=1 ./Defold

D=2

```

Or by modifying the `Defold/config` file and on the `vmargs` line add `-Djdk.gtk.version=2`:

```
vmargs = -Djdk.gtk.version=2,-Dfile.encoding=UTF-8,...
```


#### Q: Why am I not able to browse all available file locations when I select Open From Disk?

A: If you are running Defold from [Steam using Flatpak](https://flathub.org/apps/com.valvesoftware.Steam) you need to give Steam permission to access your other drives. You can modify the permissions of your Flatpak applications using [Flatseal](https://flathub.org/apps/com.github.tchx84.Flatseal) or similar tool.


#### Q: Why am I not able to open the web profiler or any other menu option which requires a browser?

A: It is likely that an internal call to `Desktop.getDesktop().browse(new URI(url));` fails since no browser is detected on non-Gnome systems. Try installing `libgnome`.

```bash
$ apt-get install libgnome
```