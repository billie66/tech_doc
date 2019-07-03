## create-react-app errors

### cann't create new app
when create a react app with create-react-app, run command:

```
yarn create react-app my-app
```

then get the following error:

```
yarn create v1.13.0
[1/4] 🔍  Resolving packages...
[2/4] 🚚  Fetching packages...
[3/4] 🔗  Linking dependencies...
[4/4] 🔨  Building fresh packages...
success Installed "create-react-app@3.0.1" with binaries:
      - create-react-app
internal/modules/cjs/loader.js:583
    throw err;
    ^

Error: Cannot find module 'rxjs'
    at Function.Module._resolveFilename
(internal/modules/cjs/loader.js:581:15)
    at Function.Module._load (internal/modules/cjs/loader.js:507:25)
    at Module.require (internal/modules/cjs/loader.js:637:17)
    at require (internal/modules/cjs/helpers.js:22:18)
    at Object.<anonymous>
(/Users/peter/.config/yarn/global/node_modules/create-react-app/node_modules/inquirer/lib/ui/prompt.js:3:34)
    at Module._compile (internal/modules/cjs/loader.js:689:30)
    at Object.Module._extensions..js (internal/modules/cjs/loader.js:700:10)
    at Module.load (internal/modules/cjs/loader.js:599:32)
    at tryModuleLoad (internal/modules/cjs/loader.js:538:12)
    at Function.Module._load (internal/modules/cjs/loader.js:530:3)
```

Fixed the error as follows:

* update yarn version
* then run commands: `yarn cache clean`

### cann't access localhost

fixed: flush DNS cache, run below command on MacOs 10.10.4 and above

```
sudo killall -HUP mDNSResponder
```

