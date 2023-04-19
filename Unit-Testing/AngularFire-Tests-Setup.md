# Follow this guide if you generated your Angular Project without tests
In this guide, we will setup tests manually for an existing Angular Project


**Summary:**
1. Create `test.ts` file
2. Create `tsconfig.spec.json`
6. Update `tslint.json`
3. Install dependencies that are required for tests
5. Update `.gitignore`
1. Update `angular.json`
1. Create `karma.conf.js` and `karma.ci.conf.js` files
1. `package.json` updates
4. Create `/tests` directory and your test files


## test.ts
In the root of the `/src` folder create a new file `test.ts` with the following content:

```
// This file is required by karma.conf.js and loads recursively all the test files located in the `/tests` folder
import 'zone.js/dist/zone-testing';
import { getTestBed } from '@angular/core/testing';
import {
  BrowserDynamicTestingModule,
  platformBrowserDynamicTesting
} from '@angular/platform-browser-dynamic/testing';

declare const require: any;

// First, initialize the Angular testing environment.
getTestBed().initTestEnvironment(
  BrowserDynamicTestingModule,
  platformBrowserDynamicTesting()
);
// Then we find all the tests.
const context = require.context('../tests', true, /\.ts$/);
// And load the modules.
context.keys().map(context);
```

This file will be the entry point of your test classes

---

## tsconfig.spec.json
In the root of your angular app (same level with `src`) create a new json file: `tsconfig.spec.json` with the following content:
```
{
  "extends": "./tsconfig.json",
  "compilerOptions": {
    "outDir": "./out-tsc/spec",
    "types": [
      "jasmine",
      "node"
    ]
  },
  "files": [
    "src/test.ts",
    "src/polyfills.ts"
  ],
  "include": [
    "tests/**/*.ts"
  ]
}
```
This file will be responsible for compiling your test files/classes (`.ts`). Notice the `"include"` property having the value `"tests/**/*.ts"`. This value should always point to the directory where your test classes are written

## tslint.json
This file is already existing in the root of your angular app. Look for the property called `"linterOptions"`, and it's child property `"exclude"` (array). Add a new value `"tests/**/*.ts"` so that your test classes won't be `tslint`-ed. Your file should look very similar to this:
```
...
"linterOptions": {
      "exclude": [
          ".node_modules",
          "src/*.ts",
          "tests/**/*.ts"
      ]
},
...
```

## Installing test dependencies
You can add these dependencies manually to your `package.json` file or just install them manually using `npm i`. Make sure to save them as `devDependencies` or use the `--save-dev` flag.

Command:
```
npm i --save-dev @types/jasmine @types/jasminewd2 jasmine-core jasmine-spec-reporter karma karma-chrome-launcher karma-coverage-istanbul-reporter karma-jasmine karma-jasmine-html-reporter
```

1. `Karma` - Test Runner. Very similar to Mocha
2. `Jasmine` - All around framework as assertion library, test runner, stubbing/spying library
3. `Instanbul` - Code Coverage Reporter/Viewer


## .gitignore updates
There are some files generated when running tests such as the code coverage page, logs, and etc. These files shouldn't be committed to the repository

In your `.gitignore` file, add 2 new lines:
`*/debug.log`
`*/coverage`


## angular.json updates
This file is 101% existing; Look for the property called `"lint"`. Below or above it add a new property called `"test"` with the following definition:

```
"test": {
          "builder": "@angular-devkit/build-angular:karma",
          "options": {
            "main": "src/test.ts",
            "polyfills": "src/polyfills.ts",
            "tsConfig": "tsconfig.spec.json",
            "karmaConfig": "karma.conf.js",
            "assets": [
              "src/favicon.ico",
              "src/assets"
            ],
            "styles": [
              "src/styles.scss"
            ],
            "scripts": []
          }
        }
```
This will tell the `Angular CLI`, that we want it to test our application. The `test` maps to the `ng` CLI command `ng test`. This command reads the definition


## karma config files
The `karma.conf.js` will contain obviously the configuration for your test runner. Put it into the root of your app, at the same level of your `package.json` file. The content should be:

```
module.exports = function (config) {
  config.set({
    basePath: '',
    frameworks: ['jasmine', '@angular-devkit/build-angular'],
    plugins: [
      require('karma-jasmine'),
      require('karma-chrome-launcher'),
      require('karma-jasmine-html-reporter'),
      require('karma-coverage-istanbul-reporter'),
      require('@angular-devkit/build-angular/plugins/karma')
    ],
    client: {
      clearContext: false // leave Jasmine Spec Runner output visible in browser
    },
    coverageIstanbulReporter: {
      dir: require('path').join(__dirname, './coverage/angular-tests'),
      reports: ['html', 'lcovonly', 'text-summary'],
      fixWebpackSourcePaths: true
    },
    reporters: ['progress', 'kjhtml'],
    port: 9876,
    colors: true,
    logLevel: config.LOG_INFO,
    autoWatch: true,
    browsers: ['Chrome'],
    singleRun: false,
    restartOnFileChange: true
  });
};
```

The `karma.ci.conf.js` is an alternate `karma` config that changes the `browser` to a Headless and enforces `singleRun` (non-debugging test runs). This will be used by the `CI` so that the test will be ran more efficiently. The file content should be:

```
module.exports = function (config) {
  config.set({
    basePath: '',
    frameworks: ['jasmine', '@angular-devkit/build-angular'],
    plugins: [
      require('karma-jasmine'),
      require('karma-chrome-launcher'),
      require('karma-jasmine-html-reporter'),
      require('karma-coverage-istanbul-reporter'),
      require('@angular-devkit/build-angular/plugins/karma')
    ],
    client: {
      clearContext: false // leave Jasmine Spec Runner output visible in browser
    },
    coverageIstanbulReporter: {
      dir: require('path').join(__dirname, './coverage/angular-tests'),
      reports: ['html', 'lcovonly', 'text-summary'],
      fixWebpackSourcePaths: true
    },
    reporters: ['progress', 'kjhtml'],
    port: 9876,
    colors: true,
    logLevel: config.LOG_INFO,
    autoWatch: true,
    browsers: ['ChromeHeadless'],
    singleRun: true,
    restartOnFileChange: true
  });
};
```


## package.json updates
Update your `package.json`, look for the `"scripts"` property and add 2 new commands:

```
"test": "ng test --code-coverage true",
"test-ci": "ng test --karma-config karma.ci.conf.js"
```

The `test` command (ran by `npm run test`) shall be the command used for running tests locally. It will open a browser (Chrome) that will show your test runs (test cases) that should also allow you to debug your test.

The `test-ci` command is expected to be ran by your `CI`. This is a light-weight version of the command where the Browser won't be launched and the test won't enter debug mode (by using a different karma.conf.js`)


## /tests directory and test files
Your folder structure in `src` should be adapted in your `tests` folder. For obvious reasons, you can easily locate your tests.

Sample Test Class:
```
import { AlertService } from 'src/app/_services';
import { AbstractListComponent, AbstractListService } from "src/app/_shared/components/abstracts";
import { AbstractListComponentOptions, ListViewModel } from 'src/app/_shared/models';

describe('AbstractListComponent', () => {
  let target: AbstractListComponent<ListViewModel>;
  let alertServiceSpy: jasmine.SpyObj<AlertService>;
  let listServiceSpy: jasmine.SpyObj<AbstractListService<ListViewModel>>;
  let options: AbstractListComponentOptions;

  beforeEach(() => {
    alertServiceSpy = jasmine.createSpyObj<AlertService>('AlertService', ['alert', 'confirm']);
    listServiceSpy = jasmine.createSpyObj<AbstractListService<ListViewModel>>('AbstractListService', ['archive', 'restore', 'getAudit', 'getArchived']);
    options = {
      messages: {
        confirmation: {
          archive: {
            primary: '',
            secondary: ''
          },
          restore: {
            primary: '',
            secondary: ''
          }
        }
      }
    };

    target = new AbstractListComponent<ListViewModel>(alertServiceSpy, listServiceSpy, options);
  });

  describe('constructor', () => {
    it('should set activeTab to audit', () => {
      expect(target.activeTab).toEqual('audit');
    });
  });

  describe('initData', () => {
    describe('activeTab is set to audit', () => {
      const auditMockData: ListViewModel[] = [{ id: '1', selected: false }, { id: '2', selected: false }];

      beforeEach(async () => {
        listServiceSpy.getAudit.and.returnValue(Promise.resolve(auditMockData));
        target.setTab('audit');
        await target.initData();
      });

      it('should set the sort mode to default', () => {
        expect(target.sortMode).toEqual('default');
      });

      it('should set objects to the resolved value of service.getAudit', () => {
        expect(target.objects).toEqual(auditMockData);
      });

      it('should set _objects', () => {
        expect(target._objects).toBeDefined();
      });
    });

    describe('activeTab is set to archive', () => {
      const archiveMockData: ListViewModel[] = [{ id: '1', selected: false }, { id: '2', selected: false }];

      beforeEach(async () => {
        listServiceSpy.getArchived.and.returnValue(Promise.resolve(archiveMockData));
        target.setTab('archive');
        await target.initData();
      });

      it('should set the sort mode to default', () => {
        expect(target.sortMode).toEqual('default');
      });

      it('should set objects to the resolved value of service.getAudit', () => {
        expect(target.objects).toEqual(archiveMockData);
      });

      it('should set _objects', () => {
        expect(target._objects).toBeDefined();
      });
    });
  });

  describe('processObjects', () => {
    describe('no objects selected', () => {
      beforeEach(() => {
        target.objects = [{ selected: false, id: '1' }];
      });

      it('should not throw any errors', async () => {
        expect(async () => target.processObjects('archive')).not.toThrow();
      });
    });
  });
});
```


