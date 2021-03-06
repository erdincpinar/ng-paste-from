# ng-paste-from

AngularJS directive that converts pasted plain text tabular data to an array of arrays/objects on the scope.

## Demo

[Try a demo of ng-paste-from.](http://digiexam.github.io/ng-paste-from/)

## Example HTML

	<textarea
		id="excel-paste"
		ng-paste-from="users" 
		ng-paste-from-columns="['name', 'email']" 
		ng-paste-from-on-validate="onValidate"
		ng-paste-from-on-error="onError"></textarea>

NOTE: It is important that the element that has the ng-paste-from directive supports newlines, otherwise they get excluded and the parse becomes invalid.

## Dependencies

Major version 3 depends on Angular ~1.3.11.

Major versions 1 and 2 depend on Angular ~1.2.6.

## Attributes

### `ng-paste-from`

* Type: variable binding

The variable on the scope that should be assigned the parsed result.

The format of the parsed result depends on `ng-paste-from-columns`,
look at that attribute for more information.

### `ng-paste-from-columns`

#### Type: `Array`

* Example: `ng-paste-from-columns="['name', 'email']"`
* **Parsed result:** an array of row objects.
* **Parsed result example:** `[{"name": "a", "email": "a@a.a"},{"name": "b", "email": "b@b.b"}]`

The arrays length becomes the number of columns expected by the parser.

#### Type: `Number`

* Example: `ng-paste-from-columns="2"`
* **Parsed result:** an array of row arrays (each array item is a column)
* **Parsed result example:** `[["a", "a@a.a],["b", "b@b.b"]]`

It's the number of columns expected by the parser.

### `ng-paste-from-row-separator`

* Type: `RegExp`, `String`
* Default value: <code>/\r\n&#124;\n\r&#124;\n&#124;\r/g</code>
 
Used to split the pasted data into rows.

### `ng-paste-from-column-separator`

* Type: `RegExp`, `String`
* Default value: `"\t"`
             
Used to split the rows into columns.

### `ng-paste-from-paste-only`

* Type: `Boolean`
* Default value: `true`
             
Only allow pasting into the source element.

### `ng-paste-from-before-parse`

* Type: `Function`
* Signature: `beforeParse(data)`
* **Return:** the data, or else nothing will be parsed.

Callback to manipulate the data before it is parsed.

### `ng-paste-from-on-validate`

* Type: `Function`
* Signature: `onValidate(row, rowData)`
* Arguments:
  * row: (Object or Array) See the `ng-paste-from-columns` option for details on this value
  * rowData: (Object)
    * index: (Number, Int) Index of the row in the split source text, before trimming empty lines
    * source: (String) Row source text
    * expectedLength: (Number, Int) Expected number of columns in the row
    * actualLength: (Number, Int) Actual number of columns in the row

Callback to validate a row object or array.

See the `ng-paste-from-columns` attribute for more details on when a row will
be an object or an array.

### `ng-paste-from-on-error`

* Type: `Function`
* Signature: `onError(error, rowData)`
* Arguments:
  * error: (String) Name of the error, see the Errors section of this README
  * rowData: (Object)
    * index: (Number, Int) Index of the row in the split source text, before trimming empty lines
    * source: (String) Row source text
    * expectedLength: (Number, Int) Expected number of columns in the row
    * actualLength: (Number, Int) Actual number of columns in the row

Callback to handle errors.

## Errors passed to the on error callback

Error | Description
--- | ---
NGPASTEFROM_INVALID_COLUMN_LENGTH | The processed row does not have the correct number of columns 
NGPASTEFROM_FAILED_VALIDATION | The processed row failed validation 

## Getting started with development

1. Install NodeJS ([nodejs.org](http://nodejs.org/))
2. Install Gulp globally: `npm install -g gulp`
3. Fork the repo and clone it. ([How to do it with GitHub.](https://help.github.com/articles/fork-a-repo))
4. Go into the project folder: `cd ng-paste-from`
5. Install the project dependencies: `npm install`
6. Build the project files: `gulp`
  * Build them whenever they change: `gulp watch`

To make development of ng-paste-from easier you can check out the `master` branch in one directory and the `gh-pages` branch in another, then symlink the dist files from `master` into the `lib` directory in `gh-pages`, and change the includes in `index.html` to use those versions.

## Browser compatability

Chrome, Firefox, Safari and IE9+

## License

Licensed under [MIT](LICENSE)

Copyright (C) 2014 DigiExam
