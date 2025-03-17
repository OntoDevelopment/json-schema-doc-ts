# json-schema-doc

**NOTE:** This module supports [json-schema.org](https://json-schema.org/) `draft-7`. Previous drafts may not generate documentation correctly.

## Generate markdown documentation for JSON Schemas
[Click here](https://github.com/BrianWendt/json-schema-md-doc/tree/master/samples/node) to see the Node example.

If you just need to quickly create markdown from a JSON schema, use the [online tool](https://brianwendt.github.io/json-schema-md-doc/).

### Simple Implementation

**es6 and later**

```
npm install json-schema-md-doc
```

```javascript
import { JSONSchemaMarkdownDoc } from "json-schema-doc";

// simple schema for the example
const colors_schema = {
	"description": "Choose a color",
	"type": "string",
	"enum": ["red", "amber", "green"]
}

// create an instance of JSONSchemaMarkdownDoc and load the schema
const Doccer = new JSONSchemaMarkdownDoc(colors_schema);
// generate the markdown
console.log(Doccer.generate());
```

**Result**

```markdown
*Choose a color*

Type: `string`

*path: #*

The value is restricted to the following: 

 1. *"red"*
 2. *"amber"*
 3. *"green"*

*Generated with [OntoDevelopment/json-schema-doc](https://github.com/OntoDevelopment/json-schema-doc)*
```

### Extendabale

You may easily extend `JSONSchemaMarkdownDoc` to customize the formatting of your markdown by overriding any method.

```typescript
import { JSONSchemaMarkdownDoc } from "json-schema-doc";

class MyDoccer extends JSONSchemaMarkdownDoc {
    footer = "Thanks for reading the documentation!";
    valueBool(bool: boolean | string) {
        if (typeof bool === "string") {
            return bool;
        } else {
            return bool ? "TRUE" : "FALSE"; //uppercase instead of true/false
        }
    }
}
```

## Generate documentation in other formats for JSON Schemas
This project may add a JSONSchemaHtmlDoc (JSON Schema to HTML documentation) class in the future. This is a small sample of what that might look like.
```typescript
import { JSONSchemaDocAbstract } from "json-schema-doc";

class JSONSchemaHtmlDoc extends JSONSchemaDocAbstract {
    writeLine(text: string = "", level: number = 1): this {
        this.response += '<p style="padding-left: ' + level + 'em">' + text + '</p>';
        return this;
    }
    // ... 
}
```
