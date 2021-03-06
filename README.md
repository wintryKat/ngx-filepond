# Angular FilePond

Angular FilePond is a handy adapter component for [FilePond](https://github.com/pqina/filepond), a JavaScript library that can upload anything you throw at it, optimizes images for faster uploads, and offers a great, accessible, silky smooth user experience.

## Installation

Install FilePond component from npm.

```bash
npm install filepond @thewintrykat/ngx-filepond --save
```

Import `FilePondModule` and if needed register any plugins. Please note that plugins need to be [installed from npm](https://pqina.nl/filepond/docs/patterns/plugins/introduction/#installing-plugins) separately.

Add FilePond styles path `./node_modules/filepond/dist/filepond.min.css` to the `build.options.styles` property in `angular.json`

```ts
// app.module.ts
import { BrowserModule } from '@angular/platform-browser';
import { NgModule } from '@angular/core';
import { AppComponent } from './app.component';

// import filepond module
import { FilePondModule, registerPlugin } from '@thewintrykat/ngx-filepond';

// import and register filepond file type validation plugin
import FilePondPluginFileValidateType from 'filepond-plugin-file-validate-type';
registerPlugin(FilePondPluginFileValidateType);

@NgModule({
  declarations: [
    AppComponent
  ],
  imports: [
    BrowserModule,
    FilePondModule // add filepond module here
  ],
  providers: [],
  bootstrap: [AppComponent]
})
export class AppModule { }
```

```html
<!-- app.component.html -->
<file-pond #myPond 
    [options]="pondOptions" 
    [files]="pondFiles"
    (oninit)="pondHandleInit()"
    (onaddfile)="pondHandleAddFile($event)"
    (onactivatefile)="pondHandleActivateFile($event)">
</file-pond>
```

```ts
// app.component.ts
import { Component, ViewChild } from '@angular/core';
import { FilePondComponent } from '@thewintrykat/ngx-filepond';
import { FilePondOptions } from 'filepond';

@Component({
  selector: 'app-root',
  templateUrl: './app.component.html',
  styleUrls: ['./app.component.css']
})

export class AppComponent {

  @ViewChild('myPond') myPond: FilePondComponent

  pondOptions: FilePondOptions = {
    allowMultiple: true,
    labelIdle: 'Drop files here...'
  }

  pondFiles: FilePondOptions["files"] = [
    {
      source: 'assets/photo.jpeg',
      options: {
        type: 'local'
      }
    }
  ]

  pondHandleInit() {
    console.log('FilePond has initialised', this.myPond);
  }

  pondHandleAddFile(event: any) {
    console.log('A file was added', event);
  }

  pondHandleActivateFile(event: any) {
    console.log('A file was activated', event)
  }

}

```

[Read the docs for more information](https://pqina.nl/filepond/docs/patterns/frameworks/angular/)
