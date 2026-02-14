# fpx

Run Flatpak applications using shorter names, because why type `flatpak run com.obsproject.Studio`,
when you can instead type `fpx obs`?

All in a single Python script, no external dependencies.

## Requirements

- Python 3.9+
- Flatpak

## Install

Simply download, or clone and move (or symlink) the `fpx` script to somewhere on your PATH, such
as `~/.local/bin`. It's a single Python script, no external dependencies.

## Usage

To see a list of the Flatpak aliases, simply run `fpx --list`

```sh
# Sample output -- yours will depend on what Flatpaks you have installed.
audacity -> org.audacityteam.Audacity
firefox -> org.mozilla.firefox
kdiff3 -> org.kde.kdiff3
obs -> com.obsproject.Studio
obsidian -> md.obsidian.Obsidian
```

fpx primary selects aliases based on the application manifest's "command" attribute (i.e. the name
of the actual binary that runs inside the Flatpak sandbox). This should, theoretically, result in
more "natural" aliases, ideally matching what you'd get if you installed the latest package.

Other fallback techniques and a set of manual overrides are also used, in cases where the automatic
alias detection yields unhelpful results.

You can test an alias with `fpx --print <alias>` or `fpx --test <alias>`, which will print the
matching Flatpak ID or the full `flatpak run` command respectively.

```sh
$ fpx --print vlc
org.videolan.VLC (system)
$ fpx --test vlc
/usr/bin/flatpak --system run org.videolan.VLC --
```

To run a Flatpak, simply pass it as the first argument. Command-line arguments will be forwarded
to the Flatpak where possible.

```sh
$ fpx vlc
```

You can also use the `-d`/`--detach` flag to run the Flatpak in the background without blocking
the current shell:

```sh
$ fpx -d vlc
```

> [!NOTE]
> Currently, argument parsing is done in a very crude way. It works okay for passing in a `--help`
> flag or a filename, but you might find some edge cases where passed args might be absorbed by
> `fpx` or the `flatpak` CLI itself.
> 
> Contributions to improve this are welcome.

## License and Additional Notes

fpx is [open source software](https://opensource.org/osd), and is licensed under the
[Mozilla Public License, v. 2.0](https://www.mozilla.org/en-US/MPL/2.0/).
See [LICENSE.txt](LICENSE.txt).

![fpx is a Brainmade project.](https://brainmade.org/88x31-dark.png)

fpx is a [Brainmade](https://brainmade.org/) project. None of the source code was written with
generative AI.