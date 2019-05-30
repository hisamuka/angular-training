# 1. Dependencies
- `npm install typescript --save`

# 2. General Notes
## 2.1 - Class 1
- Added file `tsconfig.json` that contains the settings of TypeScript (which files to compile, output directory, etc)
- Added the option `"noEmitOnError": true` in `tsconfig.json`
    - Thus, JS codes are only generated from TS codes when there is no **compilation errors**.
- Added the following directive inside target *"scripts"* in `package.json`:
    ```
    "compile": "tsc",
    "start": "tsc -w"
    ```
- Now, to compile the TS codes, just: `npm run compile`
- However, when execute `npm start`, the tsc will be *watching* the TS codes (configured in tsconfig.json`).
    - If any code was changed, it automatically compiles the code.

- Open the view/page: `app/index.html`