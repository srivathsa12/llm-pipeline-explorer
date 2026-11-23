# LLM Pipeline Explorer

A one-page teaching tool that shows, step by step, how a language model turns text into numbers.

**Live page:** https://srivathsa12.github.io/llm-pipeline-explorer/

Everything is in a single file, `index.html`. It uses plain JavaScript with no build step, no framework, no backend and no API keys. Every section of the code starts with a `// WHAT THIS DOES:` comment written for beginners.

## What you can do

### Part 1: Tokenizer
- **Build vocabulary** from your own training sentences:
  1. Make the text lowercase.
  2. Split off punctuation (`. , ! ? '`).
  3. Split the text into words.
  4. Count each word.
  5. Number the words by frequency, with ID 0 reserved for `[UNK]`.
- **Words kept slider:** keep only the top N most frequent words. The table updates and the sentence is re-tokenized live as you drag.
- **Tokenize** a sentence into coloured chips. The colour comes from the ID, so the same word always gets the same colour. Unknown words are split into letter pieces (`z ##e ##b ##r ##a`).
- **Stats:** characters, tokens and characters per token.

### Part 2: Embeddings in 3D
- **Spelling-based mode:** every group of 3 characters is hashed into a list of 64 numbers, which is then scaled to length 1.
- **Meaning-based mode:** runs the real `Xenova/all-MiniLM-L6-v2` model in your browser with [transformers.js](https://huggingface.co/docs/transformers.js). It gives 384 numbers per sentence (mean pooling, normalised) and shows download progress.
- **PCA**, written in plain JavaScript, shrinks the numbers to x, y and z. The 3D chart is drawn with [Plotly.js](https://plotly.com/javascript/).
- **Closest pairs:** the 5 most similar sentence pairs by cosine similarity on the full vectors.
- **Try your own:** type any word or sentence to see its tokens, add it to the chart as an orange dot, and see its first 8 numbers and its 3 closest sentences.

## Things to try

- Drag **Words kept** down to 2. Common words break into pieces and the token count goes up.
- Compare **Spelling-based** with **Meaning-based**. "The cat sat on the mat." and "The bat sat on the mat." are close by spelling, while "A kitten rested on the rug." only moves close in meaning mode.
- Add `Pythons are dangerous animals`. Watch where it lands in each mode.

## Run it yourself

Open `index.html` in a browser. Spelling mode works straight away when you're online, because Plotly loads from a CDN.

Meaning mode needs the page served over http or https, so run a tiny local server:

```bash
python3 -m http.server 8000
```

Then open http://localhost:8000. If the model can't load, the page says so and uses spelling mode instead.

## Libraries (loaded from CDNs)

| Library | Version | Used for |
|---|---|---|
| Plotly.js | 4.2.0 | the 3D chart (cdn.plot.ly, with jsDelivr as a backup) |
| transformers.js | 4.3.1 | the meaning-based model (jsDelivr) |

## Author

Srivathsa Sherla, CS undergraduate (AI & Machine Learning) at Newton School of Technology.
