# FFSVGFig
A tool, still under development, to generate figures for FontForge documentation

## Dependencies

1. A python 3 installation
2. The `csscompressor` python package
3. The `svgwrite` python package

Note: This may eventually be restructured as a python package but for now it is
a bare script. 

## Options

The script must be called with two positional arguments, the first being the
pathname of a font file that FontForge can open (typically an SFD) and the 
second being the name of a glyph in that font, as in:

```
FFSVGFig doc.sfd J
```
The SVG output (in this case named `J.svg`) will depict that glyph roughly as
it is shown in FontForge's user interface. The other options are:

* `--width (-w)` The total width of the viewBox in the generated SVG. If this
  is not supplied the width will be the em-unit width of the glyph in the font
  plus twice the margin size.
* `--margin (-m)` The margin, in base SVG units, to include on each edge of the
  output glyph. Default is 20.
* `--ptmag (-t)` A scale factor for points and other FontForge notations. Can
  be floating point, default is 1.
* `--background (-b)` Whether to include contours in the background layer. 
  These will be displayed without notations and in green, as in the FontForge
  UI. Boolean. 
* `--basename (-n)` The "base name" (before the `.svg` extension) of the output
  file. Default is the glyph name.
* `--pretty (-p)` When set the output will not be "minified". Boolean. 
* `--extstyle (-e)` The filename or URL of an external style sheet to load 
  in place of an embedded style. The user must create and place the sheet in
  the right place. (Not recommended due to limited browser support for external
  SVG styles.)

## Recommended use

In general it is probably best if a document has a uniform point/notation size
close to `ptmag==1`. Therefore all figures should be generated with the same
`ptmag` and either displayed at their default size or all should be magnified
by the same factor. To choose the size of a given figure, adjust its `width`. 

Adding contours into the background of a figure and generating with the
`background` flag is a good way to illustrate before/after scenarios. See the
[Expand Stroke](https://fontforge.org/docs/techref/stroke.html) document for
examples. 

Most figures are small and most documentation is read only occasionally, so it
may be best to stick with "pretty" output. This also allows figures to be
changed with just a text editor. 

## What is and is not supported

The tool produces a relatively faithful version of quadratic or cubic contours.
The soft "interior" contour lines (usually visible at high magnification) are
not included. Closed contours are shown with a slightly green fill for clarity
while open contours are not filled. This fill can currently only be changed by
editing the style embedded in the script.

Selected on-curve points are displayed as selected so one should be careful
about which points are selected before saving the font file. (The script is
also capable of displaying selected off-curve points, but because FontForge
does not save the selection state of those points there is currently no
interface for that. However, it would be relatively easy to add a Tools menu
item to generate from the UI to get around that problem if and when needed.)

The tool does not currently display Spiro contours but they would not be very
difficult to add. Point and contour names are also not yet displayed, nor is
the Guide layer or any metric line. There is currently no way of including a
false mouse pointer for illustrative purposes, nor is there any provision for
animation. 
