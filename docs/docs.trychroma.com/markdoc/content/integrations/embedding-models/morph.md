---
name: Morph
id: morph
---

# Morph

Chroma provides a convenient wrapper around Morph's embedding API. This embedding function runs remotely on Morph's servers and requires an API key. You can get an API key by signing up for an account at [Morph](https://morphllm.com/?utm_source=docs.trychroma.com).

{% Tabs %}

{% Tab label="python" %}

This embedding function relies on the `openai` python package, which you can install with `pip install openai`.

```python
import chromadb.utils.embedding_functions as embedding_functions
morph_ef = embedding_functions.MorphEmbeddingFunction(
    api_key="YOUR_API_KEY",  # or set MORPH_API_KEY environment variable
    model_name="morph-embedding-v2"
)
morph_ef(input=["def calculate_sum(a, b):\n    return a + b", "class User:\n    def __init__(self, name):\n        self.name = name"])
```

{% /Tab %}

{% Tab label="typescript" %}

```typescript
// npm install @chroma-core/morph

import { MorphEmbeddingFunction } from '@chroma-core/morph';

const embedder = new MorphEmbeddingFunction({
    api_key: "apiKey",  // or set MORPH_API_KEY environment variable
    model_name: "morph-embedding-v2"
})

// use directly
const embeddings = embedder.generate(["function calculate(a, b) { return a + b; }", "class User { constructor(name) { this.name = name; } }"])

// pass documents to the .add and .query methods
const collection = await client.createCollection({name: "name", embeddingFunction: embedder})
const collectionGet = await client.getCollection({name: "name", embeddingFunction: embedder})
```

{% /Tab %}

{% /Tabs %}

### Code example

{% TabbedCodeBlock %}

{% Tab label="python" %}

```python
morph_ef = embedding_functions.MorphEmbeddingFunction(
    api_key="YOUR_API_KEY",  # or set MORPH_API_KEY environment variable
    model_name="morph-embedding-v2"
)

# Works with code in various languages
code_examples = [
    "def fibonacci(n):\n    if n <= 1:\n        return n\n    return fibonacci(n-1) + fibonacci(n-2)",
    "public class HelloWorld {\n    public static void main(String[] args) {\n        System.out.println(\"Hello, World!\");\n    }\n}",
    "const greeting = (name: string): string => {\n    return `Hello, ${name}!`;\n}",
    "SELECT users.name, COUNT(orders.id) as order_count\nFROM users\nLEFT JOIN orders ON users.id = orders.user_id\nGROUP BY users.id"
]

morph_ef(input=code_examples)
```

{% /Tab %}

{% Tab label="typescript" %}

```typescript
import { MorphEmbeddingFunction } from '@chroma-core/morph';

const embedder = new MorphEmbeddingFunction({
    api_key: "apiKey",  // or set MORPH_API_KEY environment variable
    model_name: "morph-embedding-v2"
})

// Works with code in various languages
const codeExamples = [
    "function fibonacci(n) { if (n <= 1) return n; return fibonacci(n-1) + fibonacci(n-2); }",
    "public class HelloWorld { public static void main(String[] args) { System.out.println(\"Hello, World!\"); } }",
    "const greeting = (name: string): string => { return `Hello, ${name}!`; }",
    "SELECT users.name, COUNT(orders.id) as order_count FROM users LEFT JOIN orders ON users.id = orders.user_id GROUP BY users.id"
]

const embeddings = embedder.generate(codeExamples)
```

{% /Tab %}

{% /TabbedCodeBlock %}

For further details on Morph's models check the [documentation](https://docs.morphllm.com/api-reference/endpoint/embedding?utm_source=docs.trychroma.com).