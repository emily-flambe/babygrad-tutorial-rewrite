# babygrad Tutorial Guidelines

## Content Replication Approach

**IMPORTANT: Faithfully replicate the original zekcrates tutorial.**

When creating or updating chapter content:
1. **Fetch the original HTML** directly from `https://zekcrates.quarto.pub/deep-learning-library/`
2. **Extract the main content** from between `<main class="content">` and `</main>`
3. **Convert Quarto markup** to our simpler HTML format:
   - Quarto callouts → `<div class="hint">` or `<div class="note">`
   - Quarto code blocks → simple `<pre><code>` blocks
   - Keep all text, code, and explanations intact
4. **Do not add, remove, or paraphrase content** - replicate it faithfully

### Original URL Mapping

| Local file | Original URL |
|------------|--------------|
| index.html | /index.html (Preface) |
| intro.html | /intro.html (Ch 1: Introduction) |
| tensor.html | /chapter1.html (Ch 2: Tensor) |
| autograd.html | /chapter2.html (Ch 3: Automatic Differentiation) |
| nn.html | /nn.html (Ch 4: nn) |
| optim.html | /optim.html (Ch 5: Optimizer) |
| data.html | /data.html (Ch 6: Data Handling) |
| init.html | /initialization.html (Ch 7: Initialization) |
| saving.html | /model_saving.html (Ch 8: Model Persistence) |
| trainer.html | /trainer.html (Ch 9: Trainer) |
| cnn.html | /cnn.html (Ch 10: Convolutional NN) |
| solutions.html | /solutions.html (Ch 11: Solutions) |
| examples.html | /examples.html (Ch 12: Examples) |
| conclusion.html | /conclusion.html (Ch 13: Conclusion) |

## File Organization

- `/public/` — Tutorial HTML files (14 chapters + styles + JS)
- `/public/styles.css` — Shared stylesheet
- `/public/copy.js` — Code block copy-to-clipboard functionality
- `wrangler.toml` — Cloudflare Workers config
- `CLAUDE.md` — This file

The actual babygrad implementation lives in a separate repo: `emily-flambe/deep-learning-library`

## babygrad Library Architecture

The tutorial teaches building a from-scratch deep learning library. The dependency chain is:

```
tensor.py → ops.py → init.py → nn.py → optim.py → data.py → trainer.py
```

### Module/File Structure (as taught)

```
babygrad/
├── __init__.py      # Exports: Tensor, ops
├── tensor.py        # Tensor class with autograd (backward, factory methods)
├── ops.py           # Function base class + all ops (Add, Mul, MatMul, Conv, etc.)
├── init.py          # Xavier/Kaiming initialization functions
├── nn.py            # Module, Linear, Sequential, BatchNorm1d, LayerNorm1d,
│                    #   Dropout, ReLU, Sigmoid, Tanh, Flatten, SoftmaxLoss,
│                    #   Residual, Conv (nn wrapper)
├── optim.py         # Optimizer, SGD, Adam
├── data.py          # Dataset, MNISTDataset, CIFAR10Dataset, DataLoader
└── trainer.py       # Trainer class (fit/evaluate)
```

### Key Naming Conventions

- Base class for operations: `Function` (NOT `Op` or `TensorOp`)
- Op methods: `forward()` and `backward()` (NOT `compute`/`gradient`)
- Package name: `babygrad` (NOT `baby`)
- File paths: `babygrad/ops.py` (NOT `baby/ops.py`)
- Gradient zeroing: `optimizer.zero_grad()` (NOT `reset_grad`)
- Setting evaluation mode: `model.eval()` (NOT `set_inference_mode()`)
- Evaluation method: `trainer.evaluate()` (NOT `assess()`)

### Common Pitfalls When Editing

1. **Multi-line imports**: Must use parentheses or backslash for line continuation
2. **Line continuations in code blocks**: HTML `<pre><code>` preserves line breaks literally — broken Python across lines is a SyntaxError if copied
3. **Folder structure diagrams**: Must stay in sync with which files have been introduced up to that chapter
4. **Exercise numbering**: Must match the chapter number (e.g., Chapter 10 exercises are 10.x, not 2.x)
5. **Forward references**: Don't reference functions/classes before the tutorial introduces them

## Visual Verification

Use Playwright to visually verify CSS and layout changes before committing:
- Take a screenshot at wide viewport (1440px) to check margin notes and layout
- Take a screenshot at narrow viewport (768px) to check mobile collapse
- Verify no content is clipped or overlapping

## Deployment

The site auto-deploys on push to `main` via Cloudflare git integration.

**Live URL:** https://babygrad-tutorial.emily-cogsdill.workers.dev

## HTML Template

Each chapter should follow this structure:

```html
<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <title>Chapter N: Title — babygrad</title>
  <link rel="stylesheet" href="styles.css">
</head>
<body>
  <div class="container">
    <nav class="sidebar">
      <h2><a href="index.html">babygrad</a></h2>
      <ul>
        <!-- navigation items -->
      </ul>
    </nav>

    <main class="content">
      <h1>Chapter N: Title</h1>
      <!-- content from original -->

      <div class="nav">
        <a href="prev.html">← Previous</a>
        <a href="next.html">Next →</a>
      </div>

      <div class="attribution">
        <p>Original: <a href="https://zekcrates.quarto.pub/deep-learning-library/original.html">zekcrates/original</a></p>
      </div>
    </main>
  </div>
  <script src="copy.js"></script>
</body>
</html>
```

## Styling Elements

- `<div class="hint">` — for tips, notes, and supplementary info
- `<div class="note">` — for important callouts
- `<pre><code>` — for code blocks
- `<hr>` — for section breaks within a chapter

## Attribution

Every page links to the original zekcrates tutorial in the attribution section.
