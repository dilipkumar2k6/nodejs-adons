# Node.js Addon

Following are order to load files
1. .js file
2. .json file
3. <binary>.node file

A binary .node file is compiled addon module.

This list can also be printed by running following command
```
node -p require.extensions
```

## require.extensions['.js'].toString()
```
'function (module, filename) {\n  var content = fs.readFileSync(filename, \'utf8\');\n  module._compile(stripBOM(content), filename);\n}'

```

## require.extensions['.json'].toString()
```
'function (module, filename) {\n  var content = fs.readFileSync(filename, \'utf8\');\n  try {\n    module.exports = JSON.parse(stripBOM(content));\n  } catch (err) {\n    err.message = filename + \': \' + err.message;\n    throw err;\n  }\n}'

```

## require.extensions['.node'].toString()
```
'function (module, filename) {\n  return process.dlopen(module, path.toNamespacedPath(filename));\n}'

```