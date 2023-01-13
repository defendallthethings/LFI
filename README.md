# LFI
Validation:

>$file = basename(realpath($_GET['file']));
>include($file);

