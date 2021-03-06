NyaoVim Runtime API
===================

As described in [README](../README.md), many APIs are available in NyaoVim; [<neovim-component> APIs](https://github.com/rhysd/neovim-component), [Node.js APIs](https://nodejs.org/en/docs/), [Electron APIs](https://github.com/atom/electron/tree/master/docs/api), [Neovim msgpack-rpc APIs](https://neovim.io/doc/user/msgpack_rpc.html)), so many [npm packages](https://www.npmjs.com/).
In addition to them, NyaoVim offers some extra APIs.

- API in Vim script
- Subscriable events

## API in Vim script

Vim script interface is defined [in this directory](../runtime).  The directory is added to `runtimepath` at Neovim starting.  All are defined in `nyaovim#` namespace.

### `nyaovim#load_nyaovim_plugin(runtimepath)`

Load UI plugin from the `runtimepath` directory.  It searches `nyaovim-plugin` directory and HTML files in the directory.  Then load HTML files with `<link rel="import">`.

### `nyaovim#load_nyaovim_plugin_direct(html_path)`

Directly load HTML from `html_path` HTML file with `<link rel="import">`.

### `nyaovim#require_javascript_file(script_path)`

Load `script_path` JavaScript file with Node.js's `require()` function.

### `nyaovim#call_javascript_function(func_name, args)`

Call JavaScript `func_name` global function with `args`.  `args` values in Vim script will be converted to JavaScript values.

## Subscriable events

With Neovim msgpack API, you can receive rpc nortifications.

```javascript
const neovim_element = document.getElementById('neovim');
const client = neovim_element.editor.getClient();
client.on('notification', (func_name, args) => {
    switch (func_name) {
        case 'nyaovim:edit-start':
            // Do something
            break;
        default:
            break;
    }
});
```

NyaoVim defines some notifications to use internally and UI plugins can also use them.

### `nyaovim:edit-start`

This notification is sent when Neovim starts to edit some buffer.  It passes the file path to 1st argument.


