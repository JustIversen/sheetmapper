![Packagist Downloads](https://img.shields.io/packagist/dt/JustIversen/sheetmapper)
![Code size](https://img.shields.io/github/languages/code-size/JustIversen/sheetmapper)

# SheetMapper

SheetMapper provides functionality to load data from Excel sheet or plain array and apply a number of different mapper
functions to selected columns.

You only need to provide a `SplFileInfo` object as source.

Both `Illuminate\Http\File` and `Symfony\Component\HttpFoundation\File\File` extends this native PHP class.

## Installation

`composer require justiversen/sheetmapper`

## Usage examples

Provide a plain PHP array of items to map.

```php
    $data = (new \JustIversen\SheetMapper\SheetMapper)
        ->source($inputArray)
        ->modifyHeaders([
            'name in file' => 'component_name',
            'stkpris' => 'component_price',
            'beskrivelse' => 'component_description',
        ])
        ->toLower()
        ->numberToFloat(['measurement_amount'])
        ->get();
```
Or provide a SplFileInfo Excel file to map.
Here we use Laravel's default request()->file

```php
    $data = (new \JustIversen\SheetMapper\SheetMapper)
        ->source(request()->file)
        ->modifyHeaders([
            'name in file' => 'component_name',
            'stkpris' => 'component_price',
            'beskrivelse' => 'component_description',
        ])
        ->concat(['component_name', 'component_price'], '-', 'concatted_column')
        ->checkForNull()
        ->trim()
        ->get();
```

## Contributers

 - [Kim André Langholz](https://github.com/KimLangholz)
 - [Jens Just Iversen](https://github.com/JensJI)

## License
The MIT License (MIT). Please see [License File](LICENSE) for more information.
