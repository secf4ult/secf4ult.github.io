ESM (ECMAScript Module) 在 Node.js 12 中已经处于第二阶段（试验中），通过额外参数即可使用其提供的语法。

- 传入参数 `--experimental-modules`, 或 `--input-type=module` 。
- 确保文件使用文件扩展名 `.mjs`, 如果仍使用旧有的 `.js` 文件扩展名则需要在 `package.json` 中添加属性 `"type": "module"`。
- `import` 语句中也要在被导入文件后添加 `.mjs`，因为 ESM 不会自动添加文件扩展名，例如，`import bar from './bar.mjs'`.

注意：

- 目前（截止 Node.js 12.7.0 为止）还不支持导入文件夹。
- CommonJS 与 ESM 之间的互操作性还不完美，需要[额外工作][1]。
- ESM 不存在变量 `__filename` 和 `__dirname`，使用 `import.meta.url`。

##### 参考:

1. [ECMAScript Modules \| Node.js 12 Documentation](https://nodejs.org/docs/latest-v12.x/api/esm.html)
2. [Announcing a new --experimental-modules](https://medium.com/@nodejs/announcing-a-new-experimental-modules-1be8d2d6c2ff)
3. [The new ECMAScript module support in Node.js 12](https://2ality.com/2019/04/nodejs-esm-impl.html)
4. [PR on ESM implementation](https://github.com/nodejs/node/pull/26745)

[1]: https://2ality.com/2019/04/nodejs-esm-impl.html#interoperability

---

ESM (ECMAScript Module) is now phase 2 (Experimental) in Node.js 12 and can be activated with optional flag.

- Enabling `--experimental-modules` flag, or `--input-type=module` for input via stdin.
- Files ending in `.mjs`, or `.js` with adding `"type": "module"` to the nearest `package.json` file.
- Explicitly add `.mjs` in the `import` statements, because ESM doesn't add missing filename extensions, e.g, `import bar from './bar.mjs'`.

Caveat:

- Currently (as for Node.js 12.7.0) importing directories is not supported.
- Interoperability between CommonJS and ESM is still not perfect, [extra work][1] needed.
- `__filename` and `__dirname` are not available in ESM, use `import.meta.url` instead.

##### Useful Links:

1. [ECMAScript Modules \| Node.js 12 Documentation](https://nodejs.org/docs/latest-v12.x/api/esm.html)
2. [Announcing a new --experimental-modules](https://medium.com/@nodejs/announcing-a-new-experimental-modules-1be8d2d6c2ff)
3. [The new ECMAScript module support in Node.js 12](https://2ality.com/2019/04/nodejs-esm-impl.html)
4. [PR on ESM implementation](https://github.com/nodejs/node/pull/26745)

[1]: https://2ality.com/2019/04/nodejs-esm-impl.html#interoperability