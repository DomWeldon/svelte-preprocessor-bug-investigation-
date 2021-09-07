# tl;dr

If you get this error, make sure you are using `<script lang="ts">` rather than `<script lang="typescript">`. It seems that using `typescript` will cause a build error (since uncompiled typescript get sent to esbuild), whereas using `ts` causes the proper behaviour. An arbitrary string (not `ts` or `typescript`) will cause a 500 in the browser.

# Error

See commit history of this repo for changes.

## Error Summary

Installing a dependency such as `sass` breaks TypeScript support in sveltekit's preprocessor setup.

### Output from `npm run dev`

The below is my terminal output to reproduce this error.

    $ npm run dev

    > ~TODO~@0.0.1 dev
    > svelte-kit dev


    SvelteKit v1.0.0-next.164

    local:   http://localhost:3000
    network: not exposed

    Use --host to expose server to other devices on this network


    Bundling package for SSR due to resolve failure. Failed to resolve entry for package "@sveltejs/kit". The package may have incorrect main/module/exports specified in its package.json: Missing "." export in "@sveltejs/kit" package
    ^C
    
    $ npm i -D sass

    added 1 package, and audited 203 packages in 895ms

    30 packages are looking for funding
    run `npm fund` for details

    found 0 vulnerabilities
    
    $ npm run dev

    > ~TODO~@0.0.1 dev
    > svelte-kit dev



    $ npm run dev

    > ~TODO~@0.0.1 dev
    > svelte-kit dev

    > html:/home/domweldon/somewhere/on/my/filesystem/my-app/src/routes/index.svelte:2:12: error: Expected ";" but found ":"
        2 │     let name: string = "world"
        ╵             ^

    > Build failed with 1 error:
    html:/home/domweldon/somewhere/on/my/filesystem/my-app/src/routes/index.svelte:2:12: error: Expected ";" but found ":"
    Error: Build failed with 1 error:
    html:/home/domweldon/somewhere/on/my/filesystem/my-app/src/routes/index.svelte:2:12: error: Expected ";" but found ":"
        at failureErrorWithLog (/home/domweldon/somewhere/on/my/filesystem/my-app/node_modules/esbuild/lib/main.js:1451:15)
        at /home/domweldon/somewhere/on/my/filesystem/my-app/node_modules/esbuild/lib/main.js:1131:28
        at runOnEndCallbacks (/home/domweldon/somewhere/on/my/filesystem/my-app/node_modules/esbuild/lib/main.js:921:63)
        at buildResponseToResult (/home/domweldon/somewhere/on/my/filesystem/my-app/node_modules/esbuild/lib/main.js:1129:7)
        at /home/domweldon/somewhere/on/my/filesystem/my-app/node_modules/esbuild/lib/main.js:1238:14
        at /home/domweldon/somewhere/on/my/filesystem/my-app/node_modules/esbuild/lib/main.js:609:9
        at handleIncomingPacket (/home/domweldon/somewhere/on/my/filesystem/my-app/node_modules/esbuild/lib/main.js:706:9)
        at Socket.readFromStdout (/home/domweldon/somewhere/on/my/filesystem/my-app/node_modules/esbuild/lib/main.js:576:7)
        at Socket.emit (events.js:400:28)
        at Socket.emit (domain.js:470:12)
