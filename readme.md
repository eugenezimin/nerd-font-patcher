# Nerd Fonts
This is font-patcher python script (and required source files) from a Nerd Fonts release.
## Installation
* Clone this repo or its [original archive](https://github.com/ryanoasis/nerd-fonts/releases/latest/download/FontPatcher.zip)
* Requires: Fontforge, Python 3, `python-fontforge` and `argparse` packages
  * Fontforge can be installed as package
  * or on OSX via `brew install fontforge`
  * or as [AppImage](https://github.com/fontforge/fontforge/releases)
## Usage
- Usage, recommended:
```
fontforge -script font-patcher PATH_TO_FONT
```
- Usage, direct (more convenient call, if it works for you):
```
./font-patcher PATH_TO_FONT
```

> [!NOTE]
> The resulting font's family (aka font name) will be set to the original family after CamelCasing, removing whitespace and appending ` Nerd Font`. For example, `iosevka term` would become `IosevkaTerm Nerd Font`.

Full options follow, see also [**page explaining all options**](https://github.com/ryanoasis/nerd-fonts/wiki/ScriptOptions):
```
Nerd Fonts Patcher v3.1.0-6 (4.8.1) (ff 20230101)
usage: font-patcher [-h] [-v] [-s] [--variable-width-glyphs]
                    [--debug [{0,1,2,3}]] [-q] [--careful] [-ext EXTENSION]
                    [-out OUTPUTDIR] [--makegroups [{-1,0,1,2,3,4,5,6}]] [-c]
                    [--codicons] [--fontawesome] [--fontawesomeext]
                    [--fontlogos] [--material] [--octicons] [--powersymbols]
                    [--pomicons] [--powerline] [--powerlineextra] [--weather]
                    [--boxdrawing] [--configfile CONFIGFILE] [--custom CUSTOM]
                    [--dry] [--glyphdir GLYPHDIR] [--has-no-italic] [-l]
                    [--metrics {HHEA,TYPO,WIN}] [--name FORCE_NAME]
                    [--postprocess POSTPROCESS] [--removeligs]
                    [--xavgcharwidth [XAVGWIDTH]]
                    [--progressbars | --no-progressbars]
                    font

Nerd Fonts Font Patcher: patches a given font with programming and development related glyphs

* Website: https://www.nerdfonts.com
* Version: 3.1.0-6
* Development Website: https://github.com/ryanoasis/nerd-fonts
* Changelog: https://github.com/ryanoasis/nerd-fonts/blob/-/changelog.md

positional arguments:
  font                  The path to the font to patch (e.g., Inconsolata.otf)

options:
  -h, --help            show this help message and exit
  -v, --version         show program's version number and exit
  -s, --mono, --use-single-width-glyphs
                        Whether to generate the glyphs as single-width not double-width (default is double-width) (Nerd Font Mono)
  --variable-width-glyphs
                        Do not adjust advance width (no "overhang") (Nerd Font Propo)
  --debug [{0,1,2,3}]   Verbose mode (optional: 1=just to file; 2*=just to terminal; 3=display and file)
  -q, --quiet           Do not generate verbose output
  --careful             Do not overwrite existing glyphs if detected
  -ext EXTENSION, --extension EXTENSION
                        Change font file type to create (e.g., ttf, otf)
  -out OUTPUTDIR, --outputdir OUTPUTDIR
                        The directory to output the patched font file to
  --makegroups [{-1,0,1,2,3,4,5,6}]
                        Use alternative method to name patched fonts (default=1)

Symbol Fonts:
  -c, --complete        Add all available Glyphs
  --codicons            Add Codicons Glyphs (https://github.com/microsoft/vscode-codicons)
  --fontawesome         Add Font Awesome Glyphs (http://fontawesome.io/)
  --fontawesomeext      Add Font Awesome Extension Glyphs (https://andrelzgava.github.io/font-awesome-extension/)
  --fontlogos           Add Font Logos Glyphs (https://github.com/Lukas-W/font-logos)
  --material, --mdi     Add Material Design Icons (https://github.com/templarian/MaterialDesign)
  --octicons            Add Octicons Glyphs (https://octicons.github.com)
  --powersymbols        Add IEC Power Symbols (https://unicodepowersymbol.com/)
  --pomicons            Add Pomicon Glyphs (https://github.com/gabrielelana/pomicons)
  --powerline           Add Powerline Glyphs
  --powerlineextra      Add Powerline Extra Glyphs (https://github.com/ryanoasis/powerline-extra-symbols)
  --weather             Add Weather Icons (https://github.com/erikflowers/weather-icons)

Expert Options:
  --boxdrawing          Force patching in (over existing) box drawing glyphs
  --configfile CONFIGFILE
                        Specify a file path for JSON configuration file (see sample: src/config.sample.json)
  --custom CUSTOM       Specify a custom symbol font, all glyphs will be copied; absolute path suggested
  --dry                 Do neither patch nor store the font, to check naming
  --glyphdir GLYPHDIR   Path to glyphs to be used for patching
  --has-no-italic       Font family does not have Italic (but Oblique), to help create correct RIBBI set
  -l, --adjust-line-height
                        Whether to adjust line heights (attempt to center powerline separators more evenly)
  --metrics {HHEA,TYPO,WIN}
                        Select vertical metrics source (for problematic cases)
  --name FORCE_NAME     Specify naming source ('full', 'postscript', 'filename', or concrete free name-string)
  --postprocess POSTPROCESS
                        Specify a Script for Post Processing
  --removeligs, --removeligatures
                        Removes ligatures specificed in JSON configuration file (needs --configfile)
  --xavgcharwidth [XAVGWIDTH]
                        Adjust xAvgCharWidth (optional: concrete value)
  --progressbars        Show percentage completion progress bars per Glyph Set (default)
  --no-progressbars     Don't show percentage completion progress bars per Glyph Set
```
## Examples
```
./font-patcher Droid\ Sans\ Mono\ for\ Powerline.otf
./font-patcher Droid\ Sans\ Mono\ for\ Powerline.otf -s -q
./font-patcher Droid\ Sans\ Mono\ for\ Powerline.otf --use-single-width-glyphs --quiet

./font-patcher Inconsolata.otf --fontawesome
./font-patcher Inconsolata.otf --fontawesome --octicons --pomicons
./font-patcher Inconsolata.otf

./FontForge.AppImage -script /tmp/nerdfonts/font-patcher /tmp/nerdfonts/CascadiaMonoPL-Semibold.ttf --fontawesome -out /tmp
./FontForge.AppImage -script $PWD/font-patcher $PWD/CascadiaMonoPL-Semibold.ttf --octicons -out $HOME

docker run --rm -v ~/myfont/patchme:/in:Z -v ~/myfont/patched:/out:Z nerdfonts/patcher
docker run --rm -v ~/Desktop/myfont/patchme:/in:Z -v ~/Desktop/myfont/patched:/out:Z nerdfonts/patcher --fontawesome
```
Usually you want the `--complete` option.
## Further info
For more information see:
* https://github.com/ryanoasis/nerd-fonts/
* https://github.com/ryanoasis/nerd-fonts/releases/latest/
