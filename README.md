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
For example, imagine a fireworks show.  A firework is launched and you take a burst of 7 photos separated by a second or so.  A minute or so later another one is launched and you take another burst of photos, but just 6 this time.  When you upload the photos to your computer, they will probably all be in the same directory, and the file names will not make it obvious which burst is which. timebunch will detect that there are two separate bunches of tightly clustered files, and sort them into subdirectories for you.  For more details use timebunch -h.   

## stackimages - combine images as layers
  Produces the median of a set of input images after shifting them so that
  the largest bright feature is coaligned.

  Usage:
    stackimages [-b] OUTFN INFNS...
    stackimages [-a] -r RMEAN ROUT INFNS...
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
    -r --routliers   Instead of aligning the images, produce robust estimates of
                     their average and outliers.  Alignment can be done ahead of
                     time with hugin (select write remapped images in the
                     stitcher).
    -a --align       Force aligning to the largest feature even when using -r.
    -h --help        Show this and exit.
    -v --version     Print version info and exit.
