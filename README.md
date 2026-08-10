# Angelo's Resume

An elegant academic resume, compiled with LuaLaTeX. This project is inspired by
[Gennaro Parlato's CV](https://gennaro-parlato.github.io/paper/gennaroparlato-cv-en.pdf)
and it's based on
[Haofeng Yuan's CV](https://github.com/Xyz-yuanhf/yuan-resume), while referring
to the code of [Matty's Resume](https://github.com/mattyHerzig/mattys_resume).

## Usage

Quick start with
[Overleaf](https://www.overleaf.com/latex/templates/yuans-resume-template/hzkxnqxyfgnr)
for online edit and compilation, or compile on your own computer, using
[TeXStudio](https://texstudio.org/).

**Note:**

- Please compile using **LuaLaTeX** (pdfLaTeX cannot import the fonts
  correctly).
- The fonts are included in this project package, so please follow their
  copyright.

## Build Locally

This project uses custom system fonts (Sabon, Calluna, Courier) and a specific
set of LaTeX packages. To ensure a reproducible, clean compilation without
errors related to the TeXLive version, we recommend using an isolated container
via **Toolbox** or **Distrobox**.

This guide is specifically designed for users running Flatpak editors (like
TeXstudio) on immutable distributions, or for anyone who wants to keep their
host system clean.

### Container Creation and Configuration

You can recreate the entire build environment with a single command. This will
create a container named `tex-env` and install the LuaLaTeX engine along with
all the exact dependencies required by the `.sty` file.

**If you use Toolbox (recommended on Fedora):**

```bash
toolbox create -c tex-env && toolbox run -c tex-env sudo dnf install texlive-scheme-medium texlive-xifthen texlive-fontspec texlive-titlesec texlive-enumitem texlive-ragged2e texlive-changepage texlive-booktabs texlive-arydshln -y
```

**If you use Distrobox (universal alternative):**

```bash
distrobox create -n tex-env -i fedora:latest && distrobox enter tex-env -- sudo dnf install texlive-scheme-medium texlive-xifthen texlive-fontspec texlive-titlesec texlive-enumitem texlive-ragged2e texlive-changepage texlive-booktabs texlive-arydshln -y
```

### Flatpak Permissions

If your LaTeX editor (e.g., TeXstudio) is installed via Flatpak, it needs
permission to communicate with the host system to run commands inside the
container; otherwise, you can skip this step.

From your host system's terminal, run:

```bash
flatpak override --user --talk-name=org.freedesktop.Flatpak org.texstudio.TeXstudio
```

_(Alternatively, you can enable the "D-Bus session bus" permission via a GUI
like Flatseal by adding `org.freedesktop.Flatpak` in the "Talk" section)._

### TeXstudio Configuration

To make the editor seamlessly use the isolated environment you just created:

1. Open TeXstudio and go to **Options > Configure TeXstudio**.
2. Check the **Show Advanced Options** box in the bottom left corner.
3. Go to the **Commands** tab and replace the corresponding lines with the
   following modified commands (make sure to use the correct command for your
   container manager):

**For Toolbox:**

- **If TeXstudio is installed via Flatpak:**
  - **PdfLaTeX:**
    `flatpak-spawn --host toolbox run -c tex-env pdflatex -synctex=1 -interaction=nonstopmode %.tex`
  - **LuaLaTeX:**
    `flatpak-spawn --host toolbox run -c tex-env lualatex -synctex=1 -interaction=nonstopmode %.tex`
  - **XeLaTeX:**
    `flatpak-spawn --host toolbox run -c tex-env xelatex -synctex=1 -interaction=nonstopmode %.tex`
- **If TeXstudio is installed natively (e.g., via pacman, dnf, apt):**
  - **PdfLaTeX:**
    `toolbox run -c tex-env pdflatex -synctex=1 -interaction=nonstopmode %.tex`
  - **LuaLaTeX:**
    `toolbox run -c tex-env lualatex -synctex=1 -interaction=nonstopmode %.tex`
  - **XeLaTeX:**
    `toolbox run -c tex-env xelatex -synctex=1 -interaction=nonstopmode %.tex`

**For Distrobox:**

- **If TeXstudio is installed via Flatpak:**
  - **PdfLaTeX:**
    `flatpak-spawn --host distrobox enter tex-env -- pdflatex -synctex=1 -interaction=nonstopmode %.tex`
  - **LuaLaTeX:**
    `flatpak-spawn --host distrobox enter tex-env -- lualatex -synctex=1 -interaction=nonstopmode %.tex`
  - **XeLaTeX:**
    `flatpak-spawn --host distrobox enter tex-env -- xelatex -synctex=1 -interaction=nonstopmode %.tex`
- **If TeXstudio is installed natively (e.g., via pacman, dnf, apt):**
  - **PdfLaTeX:**
    `distrobox enter tex-env -- pdflatex -synctex=1 -interaction=nonstopmode %.tex`
  - **LuaLaTeX:**
    `distrobox enter tex-env -- lualatex -synctex=1 -interaction=nonstopmode %.tex`
  - **XeLaTeX:**
    `distrobox enter tex-env -- xelatex -synctex=1 -interaction=nonstopmode %.tex`

### Compilation

The project requires **LuaLaTeX** because of the `fontspec` package included in
the preamble.

1. Go back to TeXstudio settings, in the **Build** tab.
2. Set the **Default Compiler** to `txs://lualatex`.
3. Click **OK**.

Now you can open the `main.tex` file (or your specific language variant) and
press the green compile button. The editor will communicate with the environment
and generate the PDF completely automatically.

## Preview

![image](https://github.com/ShyVortex/angelo-resume/blob/main/Preview/preview.png)

## License

The MIT License (MIT). Copyrighted fonts are not subjected to this License.
