[Issue 3285](https://github.com/facebook/jest/issues/3285).

```
cd packages/bar && yarn install && cd ../foo && yarn install && yarn run linklocal && yarn run jest
```

The package foo imports the linked package bar which imports react-text-mask
(I chose this lib because this is one that's causing problems for me).
foo has its babel config, but when you run jest, it'll crash with the following error:

```
$ "/Users/rav/Projects/jest-issue-3285-repro/packages/foo/node_modules/.bin/jest" 
 FAIL  __tests__/index-test.js
  ● Test suite failed to run

    Couldn't find preset "es2015" relative to directory "/Users/rav/Projects/jest-issue-3285-repro/packages/foo/node_modules/bar/node_modules/react-text-mask"
      
      at node_modules/babel-core/lib/transformation/file/options/option-manager.js:293:19
      at Array.map (native)

Test Suites: 1 failed, 1 total
Tests:       0 total
Snapshots:   0 total
Time:        1.412s
Ran all test suites.
error Command failed with exit code 1.
info Visit https://yarnpkg.com/en/docs/cli/run for documentation about this command.
```
