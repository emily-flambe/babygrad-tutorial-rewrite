# babygrad Tutorial Rewrite

A pedagogically improved rewrite of [zekcrates' Deep Learning Library tutorial](https://zekcrates.quarto.pub/deep-learning-library/).

**Live site:** https://babygrad-tutorial.emily-cogsdill.workers.dev

## What's different?

- Clearer explanations for beginners
- Concepts explained before code
- Fill-in-the-blank exercises (not copy-paste solutions)
- Explicit explanations of Python/NumPy behavior

See [CLAUDE.md](CLAUDE.md) for the pedagogical guidelines.

## Development

```bash
# Install wrangler
npm install wrangler

# Run locally
npx wrangler dev

# Deploy
npx wrangler deploy
```

## Structure

```
├── public/          # Static HTML files
│   ├── index.html   # Preface
│   ├── intro.html   # 1. Introduction
│   ├── tensor.html  # 2. Tensor (revised)
│   └── ...          # Chapters 3-13
├── wrangler.toml    # Cloudflare Workers config
└── CLAUDE.md        # Pedagogical guidelines
```

## Attribution

Based on zekcrates' tutorial. Each page links to its original source.
