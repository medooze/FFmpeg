## Installing FFmpeg

1. Type `./configure` to create the configuration. A list of configure
options is printed by running `configure --help`.

    `configure` can be launched from a directory different from the FFmpeg
sources to build the objects out of tree. To do this, use an absolute
path when launching `configure`, e.g. `/ffmpegdir/ffmpeg/configure`.

2. Then type `make` to build FFmpeg. GNU Make 3.81 or later is required.

3. Type `make install` to install all binaries and libraries you built.

### Building FFmpeg with Custom SigV4 Integrations 

1. Clone SigV4 [branch](https://github.com/murillo128/SigV4-for-AWS-IoT-embedded-sdk/tree/main) containing CMake build scripts

2. Build SigV4 library using the following commands

```shell
export SIGV4_DIR_PATH=/path/to/sigv4/
cd $SIGV4_DIR_PATH
mkdir ../BUILD && cd ../BUILD
cmake $SIGV4_DIR_PATH
make
```

3. Return to FFmpeg folder and run `configure` with the following arguments

```shell
./configure --extra-libs="-lpthread -lm -L$SIGV4_DIR_PATH/../BUILD/lib -lsigv4 -lssl" --extra-cflags="-I$SIGV4_DIR_PATH/source/include" --ld="g++" --pkg-config-flags="--static" --enable-debug --enable-gpl --disable-stripping --enable-gnutls --enable-libopus --enable-libvpx --enable-libx265 --enable-libxml2 --enable-libx264
```

If calling `configure` fails, inspect `ffbuild/config.log` for error messages.

4. Run `make`


NOTICE
------

 - Non system dependencies (e.g. libx264, libvpx) are disabled by default.
