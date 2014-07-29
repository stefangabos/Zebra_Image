##Zebra_Image

####A compact (one-file only), lightweight, image manipulation PHP library

Provides methods for performing several types of image manipulation operations. It doesn’t require any external libraries other than the GD2 extension (with which PHP usually comes pre-compiled with).

With this library you can resize, flip, rotate, crop and sharpen images. All sort of filters can also be applied to images: negate, grayscale, brightness, contrast, colorize, edgedetect, emboss, gaussian blur, selective blur, mean removal, smooth and pixelate; multiple filters can be applied at once for creating custom filters; It supports loading and saving images in the GIF, JPEG and PNG formats and preserves transparency of GIF, PNG8 and PNG24 images.

Code is heavily commented and generates no warnings/errors/notices when PHP’s error reporting level is set to E_ALL.

The cool thing about it is that it can re-size images to exact given width and height and still maintain aspect ratio by using one of the following methods:

1. the image will be scaled so that it will fit in a box with the given width and height and then it will be centered both horizontally and vertically in the box. The blank area will be filled with a specified color.

2. the image will be scaled so that it could fit in a box with the given width and height but will not be enclosed in a box with given width and height

3. after the image has been scaled so that its width and height are equal or greater than the required width and height respectively, a region of required width and height will be cropped from the top left corner of the resulted image.

4. after the image has been scaled so that its width and height are equal or greater than the required width and height respectively, a region of required width and height will be cropped from the center of the resulted image.

##Features

- can be used to resize, flip, rotate, crop and sharpen images
- filters can be applied to images: negate, grayscale, brightness, contrast, colorize, edgedetect, emboss, gaussian blur, selective blur, mean removal, smooth and pixelate; multiple filters can be applied at once for creating custom filters;
- can resize images to *exact* size by automatically cropping them
- preserves transparency of GIF, PNG8 and PNG24 images
- code is heavily commented and generates no warnings/errors/notices when PHP’s error reporting level is set to E_ALL
- has comprehensive documentation

## Requirements

PHP 5+, bundled GD 2.0.28+

## How to use

```php
<?php

    // load the image manipulation class
    require 'path/to/Zebra_Image.php';

    // create a new instance of the class
    $image = new Zebra_Image();

    // indicate a source image (a GIF, PNG or JPEG file)
    $image->source_path = 'path/to/image.png';

    // indicate a target image
    // note that there's no extra property to set in order to specify the target
    // image's type -simply by writing '.jpg' as extension will instruct the script
    // to create a 'jpg' file
    $image->target_path = 'path/to/image.jpg';

    // since in this example we're going to have a jpeg file, let's set the output
    // image's quality
    $image->jpeg_quality = 100;

    // some additional properties that can be set
    // read about them in the documentation
    $image->preserve_aspect_ratio = true;
    $image->enlarge_smaller_images = true;
    $image->preserve_time = true;

    // resize the image to exactly 100x100 pixels by using the "crop from center" method
    // (read more in the overview section or in the documentation)
    //  and if there is an error, check what the error is about
    if (!$image->resize(100, 100, ZEBRA_IMAGE_CROP_CENTER)) {

        // if there was an error, let's see what the error is about
        switch ($image->error) {

            case 1:
                echo 'Source file could not be found!';
                break;
            case 2:
                echo 'Source file is not readable!';
                break;
            case 3:
                echo 'Could not write target file!';
                break;
            case 4:
                echo 'Unsupported source file format!';
                break;
            case 5:
                echo 'Unsupported target file format!';
                break;
            case 6:
                echo 'GD library version does not support target file format!';
                break;
            case 7:
                echo 'GD library is not installed!';
                break;
            case 8:
                echo '"chmod" command is disabled via configuration!';
                break;

        }

    // if no errors
    } else echo 'Success!';

?>
```

Visit the **[project's homepage](http://stefangabos.ro/php-libraries/zebra-image/)** for more information.
