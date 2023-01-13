# LFI
Validation:
The PHP function basename() will read the path and only return the filename portion:

`$file = basename(realpath($_GET['file']));

include($file);
`

Santitization:
`while(substr_count($input, '../', 0)) {

    $input = str_replace('../', '', $input);
    
};
`
