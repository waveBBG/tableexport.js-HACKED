[![Build Status](https://travis-ci.org/clarketm/TableExport.svg?branch=master)](https://travis-ci.org/clarketm/TableExport)
# [TableExport](https://www.travismclarke.com/tableexport)
The simple, easy-to-implement plugin to export HTML tables to xlsx, xls, csv, and txt files

[TableExport](https://www.travismclarke.com/tableexport/) demo **--** [TableExport + RequireJS](https://github.com/clarketm/tableexport_requirejs_app) skeleton **--** [TableExport + Flask](https://github.com/clarketm/tableexport_flask_app) skeleton.

## Getting Started

### Download and Setup

To use this plugin, include the [jQuery](https://jquery.com) library, [FileSaver.js](https://github.com/clarketm/FileSaver.js/) script, and [TableExport.js](https://www.travismclarke.com/tableexport) plugin before the closing `<body>` tag of your HTML document:

```html
<script src="jquery.js"></script>
<script src="FileSaver.js"></script>
<script src="clipboard.js"></script>
 ...
<script src="tableexport.js"></script>
```

### Install with Bower

```shell
$ bower install tableexport.js-HACKED
```

### [CDNjs](https://cdnjs.com/libraries/TableExport)
|          | uncompressed | compressed |
| :------: | :----------: | :--------: |
|  __CSS__ |   [🔗](https://cdnjs.cloudflare.com/ajax/libs/TableExport/3.3.5/css/tableexport.css)     |  [🔗](https://cdnjs.cloudflare.com/ajax/libs/TableExport/3.3.5/css/tableexport.min.css)      |
|  __JS__  |   [🔗](https://cdnjs.cloudflare.com/ajax/libs/TableExport/3.3.5/js/tableexport.js)     |  [🔗](https://cdnjs.cloudflare.com/ajax/libs/TableExport/3.3.5/js/tableexport.min.js)      |
|  __Images__  | &mdash; |   [🔗<sup>xlsx</sup>](https://cdnjs.cloudflare.com/ajax/libs/TableExport/3.3.5/img/xlsx.svg)[🔗<sup>xls</sup>](https://cdnjs.cloudflare.com/ajax/libs/TableExport/3.3.5/img/xls.svg)[🔗<sup>csv</sup>](https://cdnjs.cloudflare.com/ajax/libs/TableExport/3.3.5/img/csv.svg)[🔗<sup>txt</sup>](https://cdnjs.cloudflare.com/ajax/libs/TableExport/3.3.5/img/txt.svg)  |

### Dependencies

#### Required:

* [jQuery](https://jquery.com) (1.2.1 or higher) `*`
* [FileSaver.js](https://github.com/clarketm/FileSaver.js/)

> `*` jQuery dependency requirement is removed as of [4.0.0-alpha.2](https://github.com/clarketm/TableExport/tree/v4.0.0-alpha.2)

#### Optional / Theming:

* [Bootstrap](http://getbootstrap.com/getting-started/#download) (3.1.0 or higher)

#### Add-Ons:
In order to provide **Office Open XML SpreadsheetML Format ( .xlsx )** support, you must include the following third-party script to your project before [FileSaver.js](https://github.com/clarketm/FileSaver.js/) and [TableExport.js](https://www.travismclarke.com/tableexport).

* [xlsx.core.js](https://github.com/clarketm/js-xlsx) by _clarketm_

```html
<script src="xlsx.core.js"></script>
<script src="FileSaver.js"></script>
<script src="clipboard.js"></script>
 ...
<script src="tableexport.js"></script>
```

#### Older Browsers:
To support older browsers ( **Chrome** < 20, **Firefox** < 13, **Opera** < 12.10, **IE** < 10, __Safari__ < 6 ) include the [Blob.js](https://github.com/clarketm/Blob.js/) polyfill before the [FileSaver.js](https://github.com/clarketm/FileSaver.js/) script.

Until [Safari](https://github.com/clarketm/FileSaver.js/issues/242) provides native support for either the [HTML5 download attribute](http://caniuse.com/#feat=download) or [service workers](http://caniuse.com/#search=service%20workers), limited `xlx` and `xlsx` support is provided by including the [Blob.js](https://github.com/clarketm/Blob.js/) polyfill, albeit the **filename** will always be labeled `Unknown`.

* [Blob.js](https://github.com/clarketm/Blob.js) by _clarketm_

```html
<script src="xlsx.core.js"></script>
<script src="Blob.js"></script>
<script src="FileSaver.js"></script>
<script src="clipboard.js"></script>
 ...
<script src="tableexport.js"></script>
```

## Usage

### CSS

By default, [TableExport.js](https://www.travismclarke.com/tableexport) utilizes the [Bootstrap](http://getbootstrap.com/getting-started/#download) CSS framework to deliver enhanced table and button styling. For non-Bootstrap projects, initialize with the `bootstrap` property set to `false`.

```js
$("table").tableExport({
    bootstrap: false
});
```

When used along with Bootstrap, there are four custom classes **.xlsx, .xls, .csv, .txt** providing button styling for each of the exportable filetypes.

### JavaScript

To use the export plugin, just call:

```js
$("table").tableExport();
```

Additional properties can be passed in to customize the look and feel of your tables, buttons, and exported data.

Notice that by default, TableExport will create export buttons for three different filetypes *xls, csv, txt*. You can choose which buttons to generate by setting the `formats` property to the filetypes of your choice.

```js
/* Defaults */
$("table").tableExport({
    headings: true,                     // (Boolean), display table headings (th/td elements) in the <thead>
    footers: true,                      // (Boolean), display table footers (th/td elements) in the <tfoot>
    formats: ["xlsx", "csv", "copy"],   // (String[]), filetype(s) for the export
    fileName: "id",                     // (id, String), filename for the downloaded file
    bootstrap: true,                    // (Boolean), style buttons using bootstrap
    position: "bottom",                 // (top, bottom), position of the caption element relative to table
    ignoreRows: null,                   // (Number, Number[]), row indices to exclude from the exported file
    ignoreCols: null,                   // (Number, Number[]), column indices to exclude from the exported file
    ignoreCSS: ".tableexport-ignore",   // (selector, selector[]), selector(s) to exclude cells from the exported file
    emptyCSS: ".tableexport-empty",     // (selector, selector[]), selector(s) to replace cells with an empty string in the exported file
    trimWhitespace: false               // (Boolean), remove all leading/trailing newlines, spaces (including non-breaking spaces), and tabs from cell text
});
```
> **Note:**  to use the xlsx filetype, you must include the third-party scripts listed in the Dependencies section.

TableExport supports additional methods (**update**, **reset** and **remove**) to control it after creation.

```js
/* Run plugin and save it to a variable */
var tables = $("table").tableExport();
```

```js
/* update */
tables.update({
    filename: "newFile"     // pass in a new set of properties
});

/* reset */
tables.reset();             // useful for a dynamically altered table

/* remove */
tables.remove();            // removes caption and buttons
```

### Properties

A table of available properties and their usage can be found **[here](https://www.travismclarke.com/tableexport/#properties)**


### Methods

A table of available methods and their usage can be found **[here](https://www.travismclarke.com/tableexport/#methods)**


### Settings

Each button is assigned a default class and default content based on its respective filetype and corresponding css styles.


```js
/* default class, content, and separator for each export type */

/* Excel Open XML spreadsheet (.xlsx) */
$.fn.tableExport.xlsx = {
    defaultClass: "xlsx",
    buttonContent: "Export to xlsx",
    mimeType: "application/vnd.openxmlformats-officedocument.spreadsheetml.sheet",
    fileExtension: ".xlsx"
};

/* Excel Binary spreadsheet (.xls) */
$.fn.tableExport.xls = {
    defaultClass: "xls",
    buttonContent: "Export to xls",
    separator: "\t",
    mimeType: "application/vnd.ms-excel",
    fileExtension: ".xls"
};

/* Comma Separated Values (.csv) */
$.fn.tableExport.csv = {
    defaultClass: "csv",
    buttonContent: "Export to csv",
    separator: ",",
    mimeType: "application/csv",
    fileExtension: ".csv"
};

/* Plain Text (.txt) */
$.fn.tableExport.txt = {
    defaultClass: "txt",
    buttonContent: "Export to txt",
    separator: "  ",
    mimeType: "text/plain",
    fileExtension: ".txt"
};

/* Copy to plain Text clipboard */
$.fn.tableExport.copy = {
    defaultClass: "copy",
    buttonContent: "Copy to clipboard",
    separator: "\t"
};
```

Below are additional defaults to support the functionality of the plugin that.

```js
/* default charset encoding (UTF-8) */
$.fn.tableExport.charset = "charset=utf-8";

/* default filename if "id" attribute is set and undefined */
$.fn.tableExport.defaultFileName = "myDownload";

/* default class to style buttons when not using bootstrap  */
$.fn.tableExport.defaultButton = "button-default";

/* bootstrap classes used to style and position the export buttons */
$.fn.tableExport.bootstrap = ["btn", "btn-default", "btn-toolbar"];

/* row delimeter used in all filetypes */
$.fn.tableExport.rowDel = "\r\n";
```

### Browser Support

|  | Chrome | Firefox | IE  | Opera | Safari * |
| :------: | :------: | :-------: | :---: | :-----: | :------: |
| __Android__ |    &#10003;   |    &#10003;    | - |   &#10003;   |  -   |
| __iOS__ |    &#10003;   |  -    | - |   -   |   &#10003;    |
| **Mac OSX**|    &#10003;   |    &#10003;    | - |   &#10003;  |   &#10003;    |
| **Windows** |    &#10003;   |    &#10003;    | &#10003; |   &#10003;   |   &#10003;    |

*only _partial_ support for `xls` and `xlsx`: requires third-party dependency ([Blob.js](https://github.com/clarketm/Blob.js/))

### Live Demo 
A live, interactive demo can be found on the **[TableExport](https://www.travismclarke.com/tableexport/#live-demo)** webpage. 
* [TableExport + RequireJS](https://github.com/clarketm/tableexport_requirejs_app) skeleton.
* [TableExport + Flask](https://github.com/clarketm/tableexport_flask_app) skeleton.

### License
[TableExport.js](https://www.travismclarke.com/tableexport) is licensed under the terms of the [MIT](http://opensource.org/licenses/mit-license.php) License

### Credits

* [John Resig](https://github.com/jeresig) - jQuery
* [SheetJS](https://github.com/SheetJS) - js-xlsx 
* [Eli Grey](https://github.com/eligrey) - FileSaver.js & Blob.js
