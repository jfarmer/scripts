# Misc. Scripts

Some miscellaneous scripts I use from time to time, too small to justify their own repository.

## Scripts <!-- omit in toc -->

- [tid-terminal](#tid-terminal)
- [compress-pdf](#compress-pdf)
- [wifi-strength](#wifi-strength)
- [create-clips](#create-clips)
- [disable-library-validation](#disable-library-validation)

## tid-terminal

Enable Touch ID authentication with sudo. The script uses macOS's built-in `bioutil` to check whether Touch ID is available. If so, it enables Touch ID authentication for `sudo` commands.

**Note**: you'll have to re-run this script every time you update macOS because Apple overwrites `/etc/pam.d/sudo`

If you want to do this manually, edit `/etc/pam.d/sudo` and make sure the first non-commented line is the following:

```text
auth       sufficient     pam_tid.so
```

I don't know whether alignment matters, but when in Rome.

## compress-pdf

Use ghostscript (the `gs` command) to compress PDFs using "ebook" compression for quality.

```console
compress-pdf ./big-paper.pdf ./compressed-paper.pdf
```

## wifi-strength

Print out S/N ratio of current WiFi network using macOS's built-in `airport` command-line tool.

Useful to combine with `say` and `watch` to find dead spots in your house/apartment, e.g.,

```console
watch -n1 'wifi-stength | say'
```

## create-clips

Use `ffmpeg` to extract clips from a larger movie. Before running, make sure to install `ffmpeg`.

It also helps to install GNU `parallel`. On a Mac:

```console
brew install ffmpeg parallel
```

Create a text file with pairs of timestamps formatted as `HH:MM:SS`. Each pair should consist of two lines, the first line being the start of the cip, the second line being the end of the clip. If you want 2 clips, you'd create a file with 4 lines. Save the file as whatever you want (e.g., `timestamps.txt`) and run:

```console
./create_clips /path/to/video.mp4 < timestamps.txt | parallel --jobs 2
```

You can change the `2` in `--jobs 2` to be any number. That controls how many clips you make in parallel.

## disable-library-validation

Remove library validation from specified application on macOS. You can use this to enable virtual webcam support for applications that disabled it, e.g.,

```console
disable-library-validation /Applications/zoom.us.app
```
