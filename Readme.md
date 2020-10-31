># Laravel Zip File Creator
<br><br><br>




>## ZipController.php
```php
<?php

namespace App\Http\Controllers;

use Illuminate\Http\Request;
use ZipArchive;
use File;

class ZipController extends Controller
{
    public function zipFile()
    {
        $zip = new ZipArchive;
        $fileName = 'myzip.zip';
        if($zip->open(public_path($fileName), ZipArchive::CREATE) === True)
        {
         $files = File::files(public_path('myfile')) ;
         foreach($files as $key => $value)
         {
            $relativeNameInZipFile = basename($value);
            $zip->addFile($value,$relativeNameInZipFile);
         }

         $zip->close();
         return response()->download(public_path($fileName));
        }
    }
}

```
<br><br><br>












>## ZipController.php
```php
use App\Http\Controllers\ZipController;
Route::get('/zip',[ZipController::class, 'zipFile']);
```
<br><br><br>



































