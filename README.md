# ES Angular 6 Bootstrap 4 Table

## ToDo List
* editable
* more method
* more events
* more handler


## Features
* create for bootstrap 4
* card view in mobile
* get json data from server
* flexible header and cell template
* support client and server pagination
* keep params on url
* easy to extend tool
* i18n

## Table of contents

* [Setup](#setup)
* [Usage](#usage)
    * [Basic Usage](#basic-usage)
    * [Search](#search)
    * [Formatter and Text Template](#formatter-and-text-template)
    * [Keep](#keep)
    * [Fetch Data From API](#fetch-data-from-api)
    * [i18n](#i18n)
* [Tool](#tool)
    * [General Search](#general-search)
    * [Advanced Search](#advanced-search)
    * [Hide Column](#hide-column)
    * [Extend Tool](#extend-tool)
* [Variable](#variable)
* [Method](#method)
* [Input](#input)
* [Output](#output)
* [Demo](#demo)

## Setup

First you need to install the npm module
````
npm install es-ng6-bs4-table
````

Then import bootstrap 4 css in angular.json
````json
{
  "styles": [
    "../node_modules/bootstrap/dist/css/bootstrap.css",
    "../node_modules/open-iconic/font/css/open-iconic-bootstrap.css"
  ]
}
````

Last import the 'HttpClientModule' and 'BsTableModule' to module
````typescript
import {NgModule} from "@angular/core"
import {HttpClientModule} from "@angular/common/http";
import {BsTableModule} from "es-ng6-bs4-table";

@NgModule{
    imports: [
        HttpClientModule,
        BsTableModule,
        //if you want to keep search result
        //RouterModule
    ],
    /* if you want to add some http interceptors
    providers: [
        {provide: HTTP_INTERCEPTORS ...}
    ]
    */
}
export class AppModule{}
````

## Usage

Client side pagination

````angular2html
<es-ng-table></es-ng-table>
````

Client side pagination structure
````typescript
Array<any>
````

Server side pagination

````angular2html
<es-ng-sd-table></es-ng-sd-table>
````

Server side pagination structure

````typescript
{
    rows: Array<any>;
    total: number;
}
````

Server side params

````typescript
{
    limit: number;
    offset: number;
    sort: string;
    order: string;
    search: string;
    query: string; //json
}
````


### Basic Usage
![image](https://tinyurl.com/yab3leox)

ts:

````typescript
export class AppComponent {
  data = [
    {id: 1, name: "Sean Johnston", score: 99, description: "d1"},
    {id: 2, name: "Morgan Davies", score: 80, description: "d2"},
    {id: 3, name: "Morgan John", score: 80, description: "d3"},
    {id: 4, name: "Tommy Walker", score: 80, description: "d4"},
    {id: 5, name: "William Lee", score: 80, description: "d5"},
    {id: 6, name: "Russell Brady", score: 80, description: "d6"},
    {id: 7, name: "Isaiah Ferguson", score: 80, description: "d7"},
    {id: 8, name: "Dominic Lynch", score: 80, description: "d8"},
    {id: 9, name: "Alberto Walls", score: 80, description: "d9"},
    {id: 10, name: "Jerry Pate", score: 80, description: "d10"},
    {id: 11, name: "Spencer Gordon", score: 79, description: "d11"},
  ]
}
````

html:

````angular2html
<div class="container-fluid">
  <h1>Basic Use</h1>
  <es-ng-table [data]="data">
    <es-ng-table-col field="state" [checkbox]="true"></es-ng-table-col>
    <es-ng-table-col title="ID" field="id"></es-ng-table-col>
    <es-ng-table-col title="Name" field="name"></es-ng-table-col>
    <es-ng-table-col title="Score" field="score"></es-ng-table-col>
    <es-ng-table-col title="Description" field="description"></es-ng-table-col>
  </es-ng-table>
</div>
````

### Formatter and Text Template
![image](https://tinyurl.com/ya7ymveu)

ts: 

````typescript
export class AppComponent {
  formatter = (value: any) => {
    return value + ' postfix'
  }
}
````

html:

````angular2html
<es-ng-table [data]="data">
    <es-ng-table-col title="Name" field="name"></es-ng-table-col>
    <es-ng-table-col title="Score" field="score">
      <ng-template #textTemplate let-row="row" let-value="value" let-index="index" let-formatter="formatter">
        <button>{{value}}</button>
      </ng-template>
    </es-ng-table-col>
    <es-ng-table-col title="Description" field="description" [formatter]="formatter"></es-ng-table-col>
</es-ng-table>
````

### Keep
![image](https://tinyurl.com/y9jmylnk)

**IMPORTANT: NEED IMPORT "RouterModule". ONLY ONE KEEP IN ONE PAGE.**

You will see url change after any params changes(like: page, size, search...)

html:

````angular2html
<es-ng-table [data]="data" [keep]="true"></es-ng-table>
````

### Fetch Data From API

html:
````angular2html
<es-ng-table url="http://domain/path">
   <es-ng-table-col field="state" [checkbox]="true"></es-ng-table-col>
   <es-ng-table-col title="ID" field="id"></es-ng-table-col>
   <es-ng-table-col title="Name" field="name"></es-ng-table-col>
</es-ng-table>
````

### i18n

The default locale is en-us. Just provide "NG_TABLE_I18N" to change locale. 

````typescript
@NgModule{
    imports: [BsTableModule],
    providers: [
        {provide: NG_TABLE_I18N, useClass: NgTableZhTwService}
    ]
}

````
Current locale support: 'zh-tw', 'en-us'

## Tool
add tool in <es-ng-table-tool-bar>
html:
````angular2html
<es-ng-table>
  <es-ng-table-tool-bar>
    <div class="row">
      <!--add tool here-->
    </div>
  </es-ng-table-tool-bar>
</es-ng-table>
````

### General Search
![image](https://tinyurl.com/y92a8m6q)
html:
````angular2html
<es-ng-table [data]="data">
    <es-ng-table-tool-bar>
      <div class="row">
        <es-ng-table-general-search></es-ng-table-general-search>
      </div>
    </es-ng-table-tool-bar>
    <es-ng-table-col title="ID" field="id"></es-ng-table-col>
    <es-ng-table-col title="Name" field="name"></es-ng-table-col>
</es-ng-table>
````

### Advanced Search
![image](https://tinyurl.com/y9dcsrvr)
You can user <ng-template #editTemplate let-col="col" let-obj="obj"> to customize form control

html:
````angular2html
<es-ng-table [data]="data">
    <es-ng-table-tool-bar>
      <div class="row">
        <es-ng-table-advanced-search></es-ng-table-advanced-search>
      </div>
    </es-ng-table-tool-bar>
    <es-ng-table-col title="ID" field="id"></es-ng-table-col>
    <es-ng-table-col title="Name" field="name">
        <ng-template #editTemplate let-col="col" let-obj="obj">
           <select class="form-control" name="{{col.field}}" [(ngModel)]="obj[col.field]">
              <option *ngFor="let row of data" [ngValue]="row.name">{{row.name}}</option>
            </select>
        </ng-template>
    </es-ng-table-col>
</es-ng-table>
````

### Hide Column
![image](https://tinyurl.com/y7hhvat4)
html:
````angular2html
<es-ng-table [data]="data">
    <es-ng-table-tool-bar>
      <div class="row col-md-12">
        <es-ng-table-hide-col></es-ng-table-hide-col>
      </div>
    </es-ng-table-tool-bar>
    <es-ng-table-col field="state" [checkbox]="true"></es-ng-table-col>
    <es-ng-table-col title="ID" field="id"></es-ng-table-col>
    <es-ng-table-col title="Name" field="name"></es-ng-table-col>
</es-ng-table>
````

### Extend Tool

create tool component with inject NG_TABLE_TOKEN

````typescript
export class NgTableGeneralSearchComponent implements OnInit {
  searchTerm: string = "";

  constructor(
    @Inject(NG_TABLE_TOKEN) private table: NgTable
  ) { }

  ngOnInit() {
    this.table.search$
      .pipe(take(1))
      .subscribe((term) =>this.searchTerm = term);
  }

  search(searchTerm: string){
    this.table.generalSearch(searchTerm);
  }

}
````

then, put this component in <es-ng-table-tool-bar>
````angular2html
<es-ng-table [data]="data">
    <es-ng-table-tool-bar>
      <es-ng-table-general-search></es-ng-table-general-search>
    </es-ng-table-tool-bar>
</es-ng-table>
````

## Variable

### NgTableComponent & NgSdTableComponent

| Name     | Type         | Default | Description |
|----------|--------------|---------|-------------|
| `data`   | Array<any>   |         | data of rows.
| `rows`   | Array<any>   | []      | current data of rows.
| `total`  | number       |         | size of total data.
| `page`   | number       | 1       | current page.
| `size`   | number       | 10      | size in a page.
| `search` | string       |         | search text, used in general search.
| `query`  | string       |         | query json, user in advanced search.
| `sort`   | string       |         | sort by field.
| `order`  | 'asc' 'desc' | 'asc'   | order.
| `url`    | string       |         | get json from url.
| `keep`   | boolean      | false   | keep search result.

### NgTableColComponent

| Name       | Type    | Default | Description |
|------------|---------|---------|-------------|
| `title`    | string  |         | th text.
| `field`    | string  |         | field name in row.
| `checkbox` | boolean | false   | is checkbox cell?
| `radio`    | boolean | false   | is radio cell?
| `hidden`   | boolean | false   | is column hidden?

## Method

### NgTableComponent & NgSdTableComponent

| Name                  | Param                      | Return     | Description |
|-----------------------|----------------------------|------------|-------------|
| `refresh`             |                            | void       | refresh rows.
| `generalSearch`       | (term: string)             | void       | general search.
| `advancedSearch`      | (query: any)               | void       | advance search.
| `getSelections`       | (field: string)            | Array<any> | get selected rows.
| `hideColumn`          | (col: NgTableColComponent) | void       | hide column.
| `showColumn`          | (col: NgTableColComponent) | void       | show column.
| `toggleColumn`        | (col: NgTableColComponent) | void       | toggle column.
| `hideColumnByIndex`   | (index: number)            | void       | hide column by index.
| `showColumnByIndex`   | (index: number)            | void       | show column by index.
| `toggleColumnByIndex` | (index: number)            | void       | toggle column by index.
| `hideColumnByField`   | (field: string)            | void       | hide column by field.
| `showColumnByField`   | (field: string)            | void       | show column by field.
| `toggleColumnByField` | (field: string)            | void       | toggle column by field.


### NgTableColComponent

| Name     | Param | Return | Description |
|----------|-------|--------|-------------|
| `hide`   |       | void   | hide column.
| `show`   |       | void   | show column.
| `toggle` |       | void   | toggle column.

## Input

### NgTableComponent & NgSdTableComponent

| Name              | Type         | Default | Description |
|-------------------|--------------|---------|-------------|
| `data`            | Array<any>   |         | data of rows.
| `url`             | string       |         | get json from url.
| `sort`            | string       |         | sort by field.
| `order`           | 'asc' 'desc' | 'asc'   | order.
| `keep`            | boolean      | false   | keep search result.
| `queryFun`        | Function     |         | (client pagination) advanced search. (row: any, index: number, query: any) => Array<any>
| `responseHandler` | Function     |         | handler after get data from url. (data: any) => any


### NgTableColComponent

| Name        | Type     | Default | Description |
|-------------|----------|---------|-------------|
| `title`     | string   |         | th text.
| `field`     | string   |         | field name in row.
| `checkbox`  | boolean  | false   | is checkbox cell?
| `radio`     | boolean  | false   | is radio cell?
| `hidden`    | boolean  | false   | is column hidden?
| `formatter` | Function |         | formatter cell. (value: any) => string

## Output

### NgTableComponent & NgSdTableComponent

| Name               | Type | Description |
|--------------------|------|-------------|
| `onRowClick`       | any  | fired when row be clicked.
| `onInitKeepParams` | any  | fired when init keep params

### NgTableColComponent

| Name         | Type | Description |
|--------------|------|-------------|
| `onCellClick` | any  | fired when cell be clicked.

## Demo
````
  git clone https://github.com/endsound0211/es-ng6-bs4-table.git
  npm install
  ng serve
````
