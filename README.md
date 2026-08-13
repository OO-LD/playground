# OO-LD Playground

An interactive playground for [OO-LD](https://oo-ld.org/) schemas. It combines a JSON Schema form editor ([json-editor](https://github.com/json-editor/json-editor)) with the [JSON-LD playground](https://github.com/json-ld/json-ld.org), so a single OO-LD document can be exercised as both at once: the JSON Schema part drives validation and the generated form, the `@context` part drives the RDF output.

Live: <https://oo-ld.github.io/playground/>

## What the panes show

- **Schema** - the OO-LD document being edited (JSON). Press "Set Schema" to apply your edits.
- **Form** - the user interface generated from the schema by json-editor.
- **Data** - the JSON instance produced by the form. Press "Set Value" to push edited JSON back into the form.
- **Validation** - JSON Schema validation errors for the current instance.
- **JSON-LD** - the instance interpreted as linked data, showing the expanded form and the resulting RDF.

## The default example

The playground opens with the official OO-LD `Person` example, fetched at page load from the canonical deployment:

<https://oo-ld.org/latest/schemas/Person.schema.json>

`Person` builds on `Thing` through both `allOf` (so JSON Schema validators apply the base rules) and `@context` (so JSON-LD resolves the inherited term mappings). That pairing is the core OO-LD inheritance idiom.

Loading the example over the network rather than vendoring a copy keeps the playground in step with the specification. Because the published schemas use relative references such as `"Thing.schema.json"`, the playground rewrites them to absolute URLs against `https://oo-ld.org/latest/schemas/` before handing the document to the editor. If the deployment cannot be reached, the playground falls back to a small offline copy of the `Minimal` example and logs a warning to the browser console.

The full official example set is browsable at <https://github.com/OO-LD/oold-schema/tree/main/examples> and served under <https://oo-ld.org/latest/schemas/>. To try any of them, paste the schema into the Schema pane and press "Set Schema".

## Sharing what you built

The "Direct Link" button encodes the current schema, data and editor options into the URL as a `?data=` parameter (JSON, LZString-compressed to base64). Anyone opening that link gets your exact state. A `?data=` link always takes precedence over the default example, so shared links keep working unchanged.

"Reset Playground" clears the parameters and returns to the default example.

## Related playgrounds

| Playground | Purpose |
|---|---|
| [playground](https://oo-ld.github.io/playground/) | JSON editing mode (this one) |
| [playground-yaml](https://oo-ld.github.io/playground-yaml/) | YAML editing mode |
| [playground-python-yaml](https://oo-ld.github.io/playground-python-yaml/) | YAML mode plus in-browser Python code generation |
| [playground-awl](https://oo-ld.github.io/playground-awl/) | Abstract Workflow Language |

## Local development

This is a static page with no build step. The JSON-LD playground is included as a git submodule:

```bash
git clone --recurse-submodules https://github.com/OO-LD/playground.git
cd playground
python -m http.server
```

Then open <http://localhost:8000/>. Serving over HTTP rather than opening `index.html` directly matters, because the default example is fetched with `fetch()`.

## The legacy `examples/` directory

`examples/Person.schema.json` and `examples/Thing.schema.json` are an older copy that predates the current OO-LD conventions. They are kept only so that previously shared `?data=` links, which reference them by URL, keep resolving. Do not build on them: use the canonical schemas at <https://oo-ld.org/latest/schemas/> instead.

## More about OO-LD

- Documentation: <https://oo-ld.org/>
- Specification: <https://oo-ld.org/latest/spec/>
- Main repository: <https://github.com/OO-LD/oold-schema>
