# [directory.main.w](../../../../../../examples/tests/sdk_tests/fs/directory.main.w) | compile | tf-aws

## inflight.$Closure1-1.js
```js
module.exports = function({ $dirname, $filename, $fs_Util, $regex_Util }) {
  class $Closure1 {
    constructor({  }) {
      const $obj = (...args) => this.handle(...args);
      Object.setPrototypeOf($obj, this);
      return $obj;
    }
    async handle() {
      (await $fs_Util.mkdir($dirname));
      {((cond) => {if (!cond) throw new Error("assertion failed: fs.exists(dirname) == true")})((((a,b) => { try { return require('assert').deepStrictEqual(a,b) === undefined; } catch { return false; } })((await $fs_Util.exists($dirname)),true)))};
      try {
        (await $fs_Util.mkdir($dirname));
      }
      catch ($error_e) {
        const e = $error_e.message;
        {((cond) => {if (!cond) throw new Error("assertion failed: regex.match(\"^EEXIST: file already exists\", e) == true")})((((a,b) => { try { return require('assert').deepStrictEqual(a,b) === undefined; } catch { return false; } })((await $regex_Util.match("^EEXIST: file already exists",e)),true)))};
      }
      (await $fs_Util.writeFile((await $fs_Util.join($dirname,$filename)),""));
      const files = (await $fs_Util.readdir($dirname));
      {((cond) => {if (!cond) throw new Error("assertion failed: files.length == 1")})((((a,b) => { try { return require('assert').deepStrictEqual(a,b) === undefined; } catch { return false; } })(files.length,1)))};
      (await $fs_Util.remove($dirname,({"recursive": true})));
      {((cond) => {if (!cond) throw new Error("assertion failed: fs.exists(dirname) == false")})((((a,b) => { try { return require('assert').deepStrictEqual(a,b) === undefined; } catch { return false; } })((await $fs_Util.exists($dirname)),false)))};
      const nilFiles = (await $fs_Util.tryReaddir($dirname));
      {((cond) => {if (!cond) throw new Error("assertion failed: nilFiles == nil")})((((a,b) => { try { return require('assert').deepStrictEqual(a,b) === undefined; } catch { return false; } })(nilFiles,undefined)))};
    }
  }
  return $Closure1;
}

```

## main.tf.json
```json
{
  "//": {
    "metadata": {
      "backend": "local",
      "stackName": "root",
      "version": "0.17.0"
    },
    "outputs": {
      "root": {
        "Default": {
          "cloud.TestRunner": {
            "TestFunctionArns": "WING_TEST_RUNNER_FUNCTION_ARNS"
          }
        }
      }
    }
  },
  "output": {
    "WING_TEST_RUNNER_FUNCTION_ARNS": {
      "value": "[]"
    }
  },
  "provider": {
    "aws": [
      {}
    ]
  }
}
```

## preflight.js
```js
const $stdlib = require('@winglang/sdk');
const $plugins = ((s) => !s ? [] : s.split(';'))(process.env.WING_PLUGIN_PATHS);
const $outdir = process.env.WING_SYNTH_DIR ?? ".";
const $wing_is_test = process.env.WING_IS_TEST === "true";
const std = $stdlib.std;
const fs = $stdlib.fs;
const regex = $stdlib.regex;
class $Root extends $stdlib.std.Resource {
  constructor(scope, id) {
    super(scope, id);
    class $Closure1 extends $stdlib.std.Resource {
      constructor(scope, id, ) {
        super(scope, id);
        (std.Node.of(this)).hidden = true;
      }
      static _toInflightType(context) {
        return `
          require("./inflight.$Closure1-1.js")({
            $dirname: ${context._lift(dirname)},
            $filename: ${context._lift(filename)},
            $fs_Util: ${context._lift($stdlib.core.toLiftableModuleType(fs.Util, "@winglang/sdk/fs", "Util"))},
            $regex_Util: ${context._lift($stdlib.core.toLiftableModuleType(regex.Util, "@winglang/sdk/regex", "Util"))},
          })
        `;
      }
      _toInflight() {
        return `
          (await (async () => {
            const $Closure1Client = ${$Closure1._toInflightType(this)};
            const client = new $Closure1Client({
            });
            if (client.$inflight_init) { await client.$inflight_init(); }
            return client;
          })())
        `;
      }
      _getInflightOps() {
        return ["handle", "$inflight_init"];
      }
      _registerBind(host, ops) {
        if (ops.includes("handle")) {
          $Closure1._registerBindObject(dirname, host, []);
          $Closure1._registerBindObject(filename, host, []);
        }
        super._registerBind(host, ops);
      }
    }
    const dirname = "wingdir";
    const filename = "temp.txt";
    (fs.Util.mkdir(dirname));
    {((cond) => {if (!cond) throw new Error("assertion failed: fs.exists(dirname) == true")})((((a,b) => { try { return require('assert').deepStrictEqual(a,b) === undefined; } catch { return false; } })((fs.Util.exists(dirname)),true)))};
    try {
      (fs.Util.mkdir(dirname));
    }
    catch ($error_e) {
      const e = $error_e.message;
      {((cond) => {if (!cond) throw new Error("assertion failed: regex.match(\"^EEXIST: file already exists\", e) == true")})((((a,b) => { try { return require('assert').deepStrictEqual(a,b) === undefined; } catch { return false; } })((regex.Util.match("^EEXIST: file already exists",e)),true)))};
    }
    (fs.Util.writeFile((fs.Util.join(dirname,filename)),""));
    const files = (fs.Util.readdir(dirname));
    {((cond) => {if (!cond) throw new Error("assertion failed: files.length == 1")})((((a,b) => { try { return require('assert').deepStrictEqual(a,b) === undefined; } catch { return false; } })(files.length,1)))};
    (fs.Util.remove(dirname,({"recursive": true})));
    {((cond) => {if (!cond) throw new Error("assertion failed: fs.exists(dirname) == false")})((((a,b) => { try { return require('assert').deepStrictEqual(a,b) === undefined; } catch { return false; } })((fs.Util.exists(dirname)),false)))};
    const nilFiles = (fs.Util.tryReaddir(dirname));
    {((cond) => {if (!cond) throw new Error("assertion failed: nilFiles == nil")})((((a,b) => { try { return require('assert').deepStrictEqual(a,b) === undefined; } catch { return false; } })(nilFiles,undefined)))};
    this.node.root.new("@winglang/sdk.std.Test",std.Test,this,"test:inflight create normal directory",new $Closure1(this,"$Closure1"));
  }
}
const $App = $stdlib.core.App.for(process.env.WING_TARGET);
new $App({ outdir: $outdir, name: "directory.main", rootConstruct: $Root, plugins: $plugins, isTestEnvironment: $wing_is_test, entrypointDir: process.env['WING_SOURCE_DIR'], rootId: process.env['WING_ROOT_ID'] }).synth();

```
