# 1. Dependencies
- `npm install typescript --save`
- `npm install @types/jquery --save`

# 2. General Notes
#### Class 1
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


#### Class 2
- By default, if we don't declare types in Typescript, it assumes the implicit type `any`
- One way to force types is to add the following compiler option in `tsconfig.json`: `"noImplicitAny": true`

- We can declare the visibility of class attributes inside the class constructor:
```
// INSTEAD OF THIS
class Negociacao {
    private _data: Date;
    private _quantidade: number;
    private _valor: number;
    
    constructor(data: Date, quantidade: number, valor: number) {
        this._data = data;
        this._quantidade = quantidade;
        this._valor = valor;
    }
    ...

class Negociacao {
    constructor(private _data: Date, private _quantidade: number, private _valor: number) {}
    ...
```

- The return of the `document.querySelector` has the type `Element`.
- However, we should use specific types for the HTML dom (e.g., `HTMLInputElement`).
- Then, we should explicitly cast the return of the `document.querySelector` to them:
```
class NegociacaoController {
    private _inputData: HTMLInputElement;
    private _inputQuantidade: HTMLInputElement;
    private _inputValor: HTMLInputElement;

    constructor() {
        this._inputData = <HTMLInputElement>document.querySelector('#data');
        this._inputQuantidade = <HTMLInputElement>document.querySelector('#quantidade');
        this._inputValor = <HTMLInputElement>document.querySelector('#valor');
    }
```

#### Class 3
```
    // Similar codes
    private _negociacoes: Array<Negociacao> = [];
    private _negociacoes: Negociacao[] = [];
    
    // Similar
    private _negociacoes: Negociacoes = new Negociacoes();
    private _negociacoes = new Negociacoes(); // the type is infered
    
    // Always define the return type of a function (even if it is void)
    paraArray(): Negociacao[] {
        return [].concat(this._negociacoes);
    }
```

#### Class 4
- Abstract Classes
- **Generics = Template Classes**
```
class View<T> {
...
}

class NegociacoesView extends View<Negociacoes> {
...
}

// We still could use more than one Template
class GenericDAO<T, K> {
...
}
```

- Abstract Classes and Methods
```
abstract class View<T> {

abstract template(model: T): string;
...
}
```

### Class 5
- The problem with using libraries that are globally scoped and not created with TypeScript
- "Shut up" the compiler com `declare var`.
- The disadvantages of `declare var` with type `any`.
- The role of **TypeScript Definition**.
    - As example, we used the JQuery library inside our typescript codes.
    - We have problems concerning the true datatypes returned by the methods of JQuery (or any other libraries)
    - Thus the creators of a library can create a file called **TypeScript Declaration File**.
    - This file has information of the function and method names, and their types to be used by TypeScript.
    - Thus, based on this file, TypeScript will be able to apply static checking.
    - We can then **remove** the `declare var` used to "shut up" the compiler.
- Removing comments during compilation:
    - Just add the compiler option: `"removeComments": true` in `tsconfig.json`

