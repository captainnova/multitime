# multitime
Tools for handling files (especially images) made at different times.

## A typical workflow
1. take several exposures with a camera (burst mode is handy for this), 
2. download them to a computer,
3. group them with timebunch,
4. (optional) align the images to each other with [hugin](http://hugin.sourceforge.net/)
4. for each group, use stackimages to combine the exposures

## timebunch - groups files into bursts
timebunch sorts a set of files into subdirectories according to their timestamps by looking for gaps.
For example, imagine a fireworks show.  A firework is launched and you take a burst of 7 photos separated by a second or so.  A minute or so later another one is launched and you take another burst of photos, but just 6 this time.  When you upload the photos to your computer, they will probably all be in the same directory, and the file names will not make it obvious which burst is which. timebunch will detect that there are two separate bunches of tightly clustered files, and sort them into subdirectories for you.

Before running it the first time, or for more details, get help with timebunch
-h. The -d (dry run) option is highly recommended for tuning the gap interval
before you commit.

Example: 
After a recent lunar eclipse I sorted my many shots into subdirectories by ISO,
using gthumb and rename. I now have a directory full of ISO 640 8s exposures from
different parts of the eclipse. I want to stack close batches to improve the
signal to noise ratio, but not *all* of them together, since the Moon moved and
changed its appearance over the ~2h. Let's try 
`timebunch -t 32s -d *`
Looks good! Commit:
`timebunch -t 32s *`

## stackimages - combine images as layers
```
  Produces the median of a set of input images after shifting them so that
  the largest bright feature is coaligned.

  Usage:
    stackimages [-b] [-e P] OUTFN INFNS...
    stackimages [-a] [-c] [-e P] -r RMEAN ROUT INFNS...
    stackimages (-h | --help)
    stackimages (-v | --version)
  
  Arguments:
    OUTFN            Filename for the output
    RMEAN            Filename for the output average image
    ROUT             Filename for the output outliers image
    INFNS            Input filenames

  Options:
    -b --bkgd        (NOT YET IMPLEMENTED) Align the background instead of the
                     largest feature.
    -e P --exif=P    Look for Exif metadata in the files matching filename
                     pattern P instead of in INFNS.  Useful when INFNS is a
                     set of TIFFs remapped by hugin from a set of JPEGs matching
                     P.  Use quoting to stop the shell from expanding P.
    -r --routliers   Instead of aligning the images, produce robust estimates of
                     their average and outliers.  Alignment can be done ahead of
                     time with hugin (select write remapped images in the
                     stitcher).
    -a --align       Force aligning to the largest feature even when using -r.
                     Not recommended; use hugin or its align_image_stack instead.
    -c --colors      Weight each color seperately when using -r.  This often
                     produces strange color casts.
    -h --help        Show this and exit.
    -v --version     Print version info and exit.
```
Alternatives for astrophotography: sequator, siril

## Installation
### Requirements
- python 2.7+, python 3.6+
- docopt
- fastcluster
- numpy
- pyexiv2
- scipy

The python packages can all be installed with pip.

### Setup
#### Linux
- chmod +x stackimages timebunch
- cp stackimages timebunch to somewhere in your $PATH
#### Other OSes
?
