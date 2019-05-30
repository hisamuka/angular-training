# 1. Dependencies
- `npm install typescript --save`
- `npm install @types/jquery --save`

# 2. General Notes
#### Class 1
- Namespaces
    - Our classes "lived" in the **global scope**.
    - Now, we can group them into **Namespaces**
    - Note that it is needed to add the instruction `export` to make the classe available

    
```
namespace Views {
    export abstract class View<T> {
    ...
    }
}

// another file that uses View
namespace Views {
    export class MensagemView extends Views.View<string> {
    ...
    }
}
```

- However, we won't use Namespaces.
- Instead, we will use the `modules` scheme of EcmaScript 2015 (EC6)
- By default, all JS files are modules.
- To have access to their functions, classes, etc, we have to `export` them:
```
export abstract class View<T> {
...
}
```

- To import "things" from the modules (it has this syntax {} ):
```
import { View } from './View';
import { Negociacoes } from '../models/Negociacoes';
```

  O papel de um loader
  Levantar um servidor local
  Organização de módulo em barris