# LPG Resume

LaTeX resume built with [Awesome-CV](https://github.com/posquit0/Awesome-CV).

## Building

```bash
cd LPG
xelatex resume.tex
```

Run twice to resolve cross-references.

## Required Fonts

The build requires three font families:

- **Source Sans 3** (main document font)
- **FontAwesome** (icons)
- **Roboto** (specific sections)

### Installing Source Sans 3 (Required)

Source Sans 3 is **not** included in TeX Live (only the older Source Sans Pro is).
You must install it system-wide:

```bash
# Download Source Sans 3 static fonts from Adobe
curl -L -o /tmp/source-sans-3.zip https://github.com/adobe-fonts/source-sans/releases/download/3.052R/OTF-source-sans-3.052R.zip

# Extract and install to user fonts directory
cd /tmp
unzip -q source-sans-3.zip
cp OTF/*.otf ~/Library/Fonts/  # macOS
# or: cp OTF/*.otf ~/.local/share/fonts/  # Linux

# Refresh font cache (Linux only)
fc-cache -f ~/.local/share/fonts

# Verify installation
fc-list | grep "Source Sans 3"
```

**Important:** Install the **static OTF files**, not the variable TTF fonts.
XeLaTeX does not work properly with variable fonts.

### Installing FontAwesome and Roboto

These fonts also need to be in a `fonts/` directory within this LPG directory.

#### Option 1: TeX Live symlinks (recommended if you have TeX Live)

If you have [TeX Live](https://www.tug.org/texlive/) installed:

```bash
# From the LPG directory
mkdir -p fonts

# FontAwesome
TEXLIVE=/usr/local/texlive/2025
ln -s $TEXLIVE/texmf-dist/fonts/opentype/public/fontawesome/FontAwesome.otf fonts/

# Roboto
ROBOTO=$TEXLIVE/texmf-dist/fonts/opentype/google/roboto
for f in Roboto-Regular Roboto-Italic Roboto-Bold Roboto-BoldItalic \
          Roboto-Thin Roboto-ThinItalic Roboto-Medium Roboto-MediumItalic \
          Roboto-Light Roboto-LightItalic; do
  ln -s $ROBOTO/$f.otf fonts/
done
```

Adjust the `TEXLIVE` path if your installation year differs (e.g., `2024`).

#### Option 2: Download directly

Download and place in the `fonts/` directory:

- **FontAwesome 4.7** — [FontAwesome.otf](https://github.com/FortAwesome/Font-Awesome/releases/tag/v4.7.0)
  (download the zip, extract `fonts/FontAwesome.otf`)
- **Roboto** — [Google Fonts](https://fonts.google.com/specimen/Roboto)
  (download the family, you need: Regular, Italic, Bold, Bold Italic, Thin,
  Thin Italic, Medium, Medium Italic, Light, Light Italic)

Rename the Roboto files to match the pattern `Roboto-<Weight>.otf` if needed.
