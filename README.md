# batch-images

A couple scripts to batch convert images.

## convert-batch

A script to automate ImageMagick's `convert` command recursively in a directory.

### Options

All images in the `<source directory>` and subdirectories, except those
excluded with `-x`, are processed. If no `<output directory>` is given, the
images are converted in place.

`-s` **dimensions** (required)  
Output image dimensions, following the [Image
Geometry](http://www.imagemagick.org/script/command-line-processing.php#geometry)
format for `convert`, usually `<width>x<height>`.

`-m` **match**  
Pattern to match files for processing, default `*.jpg`.

`-l` **relative output**  
Output directory is created relative to each file. If `-x` is not given, it is
set to exclude this directory.

`-q` **quality**  
Quality, `0`-`100`, default `70`.

`-x` **exclude**  
Exclude file pattern. If `-l` is used, this defaults to exclude that path.

`-r` **RegExp**  
PERL regular expression to transform the output filenames.

`-z` **zoom**  
Zoom image to fill new ratio. Without this option the image aspect is
preserved.

`-n` **dry run**  
Print the source and output filenames without writing any files or creating any
directories.

### Examples

`convert-batch -l -d 24% export`  
Resizes all images to 24% of original (300ppi to 72ppi), and saves the new
files in a new `export` subdirectory relative to each image.

`convert-batch -d 1280x -r '/.jpg$/_1280$&/'`  
Resize all images ending in `.jpg` to 1280px wide, preserving image aspect,
and add the suffix `_1280` before the file extension.

### Requirements

ImageMagick with CLI. Install on HomeBrew on Mac with `brew install
imagemagick`.

Perl, for regular expression processing (included in most \*NIX installations,
such as GNU Linux and Mac).

## encode-batch

Use `avconv` or `ffmpeg` to encode series of images into video.

### usage

    encode-batch [-r <framerate>] [-b <bitrate>] [-e <source file extension]
    [-g] <source-path> <output-path>
