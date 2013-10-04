# convert-batch

A script to automate ImageMagick's `convert` command recursively in a directory.

## Options

**`-d` dimensions** (required)  
Output image dimensions, following the [Image
Geometry](http://www.imagemagick.org/script/command-line-processing.php#geometry)
format for `convert`, usually `<width>x<height>`.

**`-f` from**  
All images in this directory and subdirectories, except those excluded with
`-x`, are processed. Defaults to the current directory.

**`-m` match**  
Pattern to match files for processing, default `*.jpg`.

**`-o` output**  
Output directory. The subdirectory structure of the source directory will be
copied. Without this option, images are resized in place.

**`-l` relative output**  
Output directory is created relative to each file. If `-e` is not given, it is
set to exclude this directory.

**`-q` quality**  
Quality, `0`-`100`, default `70`.

**`-e` exclude**  
Exclude file pattern. If `-l` is used, this defaults to exclude that path.

**`-r` RegExp**  
PERL regular expression to transform the output filenames.

**`-z` zoom**  
Zoom image to fill new ratio. Without this option the image aspect is preserved.

**`-n` dry run**  
Print the source and output filenames without writing any files or creating any
directories.

## Examples

`convert-batch -lo export -d 24%`  
Resizes all images to 24% of original (300ppi to 72ppi), and saves the new files in
a new `export` subdirectory relative to each image.

`convert-batch -d 1280x -r '/.jpg$/_1280$&/'`  
Resize all images ending in `.jpg` to 1280px wide, preserving image aspect,
and add the suffix `_1280` before the file extension.

## Requirements

ImageMagick with CLI. Install on HomeBrew on Mac with `brew install
imagemagick`.

Perl, for regular expression processing (included in most *NIX installations,
such as GNU Linux and Mac).
