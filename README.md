# NML - Nested Markdown Language

**A structured file format for interconnected markdown content on infinite canvases**

[![Version](https://img.shields.io/badge/version-2.0-blue)](https://github.com/your-org/nml)
[![License](https://img.shields.io/badge/license-MIT-green)](LICENSE)
[![Format](https://img.shields.io/badge/format-XML-orange)](SPECIFICATION.md)

## What is NML?

NML (Nested Markdown Language) is an open XML-based file format designed for storing and organizing multiple interconnected markdown documents on infinite canvases. Think of it as a way to save complex knowledge graphs, research projects, or any collection of related markdown content with their visual relationships preserved.

### Key Features

- 🗂️ **Multi-page markdown** - Organize content across multiple connected pages
- 🔗 **Visual connections** - Link pages with typed relationships  
- 📍 **Spatial positioning** - Preserve exact layout on infinite canvas
- 🎨 **Visual organization** - Color coding and themes for content categorization
- 📷 **Image support** - Embed SVG, PNG, JPG, WEBP, and GIF images
- 🔄 **Version control friendly** - Human-readable XML format
- 🔍 **Cross-references** - Link between pages using `[[page-id]]` syntax

## Why NML?

Traditional markdown is excellent for single documents, but falls short when managing complex, interconnected content. Existing solutions either sacrifice markdown's simplicity or lack visual organization capabilities.

### The Problem
```
Research Project/
├── introduction.md
├── literature-review.md  
├── methodology.md
├── findings/
│   ├── finding-1.md
│   ├── finding-2.md
│   └── analysis.md
└── conclusions.md
```

**Issues:**
- No visual relationships between files
- Difficult to see the "big picture"
- Hard to reorganize conceptually
- Limited cross-referencing capabilities
- No spatial context or flow

### The NML Solution
```xml
<nml version="2.0">
  <!-- Single file containing all pages with spatial relationships -->
  <pages>
    <page id="intro" x="100" y="100">
      <content><![CDATA[# Introduction...]]></content>
    </page>
    <page id="lit-review" x="450" y="100">  
      <content><![CDATA[# Literature Review...]]></content>
    </page>
  </pages>
  <links>
    <link from="intro" to="lit-review" type="leads-to" />
  </links>
</nml>
```

**Benefits:**
- ✅ Visual relationships preserved
- ✅ Spatial organization maintained  
- ✅ Single file for entire project
- ✅ Full markdown compatibility
- ✅ Tool-agnostic format

## Use Cases

### 🎓 Research & Academia
- Literature reviews with connected sources
- Thesis planning and organization
- Research methodology documentation
- Grant proposal development

### 🧠 Knowledge Management
- Personal knowledge bases (PKM)
- Team documentation projects
- Learning notes and concept maps  
- Technical documentation systems

### 💼 Business & Strategy
- Strategic planning documents
- Project requirements gathering
- Process documentation
- Decision trees and workflows

### 🤖 AI-Assisted Workflows
- Organizing LLM conversation outputs
- Research synthesis from multiple sources
- Voice-to-text knowledge capture
- Collaborative AI content development

## Quick Start

### Basic Example

```xml
<?xml version="1.0" encoding="UTF-8"?>
<nml version="2.0">
  <meta 
    title="My First NML Document" 
    created="2025-01-15T10:30:00Z" 
    author="Your Name" />
  
  <canvas zoom="1.0" center-x="0" center-y="0" />
  
  <pages>
    <page id="welcome" x="100" y="100" width="300" height="200" color="blue">
      <title>Welcome to NML</title>
      <content><![CDATA[
# Welcome to NML!

This is your first NML page. You can write **full markdown** here including:

- Lists
- Links: [Example](https://example.com)  
- Images: ![Logo](./images/logo.png)
- Code blocks:

```javascript
console.log("Hello NML!");
```

Connect to other pages using: [[getting-started]]
      ]]></content>
      <tags>introduction,welcome</tags>
    </page>
    
    <page id="getting-started" x="450" y="100" width="300" height="250" color="green">
      <title>Getting Started</title>
      <content><![CDATA[
# Getting Started

Now you're ready to:

1. Create more pages
2. Connect them visually
3. Build your knowledge graph!

This page was referenced from [[welcome]].
      ]]></content>
      <tags>tutorial,next-steps</tags>
    </page>
  </pages>
  
  <links>
    <link from="welcome" to="getting-started" type="leads-to" />
  </links>
</nml>
```

### Page Colors

NML supports six color themes for visual organization:

| Color | Use Case | Example |
|-------|----------|---------|
| `red` | Urgent/Important | Critical issues, deadlines |
| `blue` | Information/Research | Data, references, facts |
| `green` | Solutions/Actions | Next steps, completed items |
| `yellow` | Questions/Ideas | Brainstorming, unknowns |
| `purple` | References/Sources | Citations, external links |
| `gray` | Archive/Completed | Finished work, deprecated |

### Connection Types

Define relationships between pages:

- `explores` - This page explores concepts from another
- `leads-to` - Natural progression of thought
- `relates` - General connection/similarity  
- `contradicts` - Opposing viewpoints
- `supports` - Evidence or examples
- `questions` - Raises questions about another page

## File Format Details

### Structure
```xml
<nml version="2.0">
  <meta>         <!-- Document metadata -->
  <canvas>       <!-- Viewport settings -->
  <pages>        <!-- Content pages -->
  <links>        <!-- Visual connections -->
</nml>
```

### Page Structure
```xml
<page id="unique-id" x="100" y="100" width="300" height="200" color="blue">
  <title>Page Title</title>
  <content><![CDATA[
    # Markdown content goes here
    
    Full CommonMark support including images and cross-references.
  ]]></content>
  <tags>tag1,tag2,tag3</tags>
</page>
```

### Images and Assets
```markdown
<!-- Relative paths from .nml file location -->
![Diagram](./images/architecture.svg)
![Screenshot](../assets/interface.png)
![Photo](./media/photo.jpg)
```

**Supported formats:** SVG, PNG, JPG, JPEG, WEBP, GIF

## Tools & Implementations

### Official Tools
- **CanvasApp** - Reference implementation (React-based canvas editor)
- **NML Validator** - Command-line validation tool
- **NML Converter** - Convert between NML and other formats

### Community Tools
- **VS Code Extension** - Syntax highlighting and validation
- **Obsidian Plugin** - Import/export NML files  
- **Notion Integration** - Convert Notion pages to NML

### Libraries
```bash
# JavaScript/TypeScript
npm install @nml/parser
npm install @nml/validator

# Python  
pip install nml-python

# Rust
cargo add nml-rs
```

## Validation

NML documents can be validated against the official specification:

```bash
# Using official validator
npx @nml/validator document.nml

# Using curl with online validator
curl -X POST -F "file=@document.nml" https://validator.nml.dev/api/validate
```

### Validation Rules
- All page IDs must be unique
- Link references must point to existing pages
- Image paths must be relative and valid
- Coordinates must be within valid ranges
- Required fields cannot be empty

## Examples

### Research Paper Planning
```xml
<nml version="2.0">
  <meta title="AI Ethics Research" tags="research,ai,ethics" />
  <pages>
    <page id="research-question" x="100" y="100" color="yellow">
      <content><![CDATA[
# Research Question
What are the ethical implications of AI in hiring?
      ]]></content>
    </page>
    <page id="literature" x="400" y="100" color="blue">
      <content><![CDATA[
# Literature Review
- Smith et al. (2023) - Bias in AI systems
- Jones (2024) - Ethical frameworks
      ]]></content>
    </page>
    <page id="findings" x="700" y="100" color="green">
      <content><![CDATA[
# Key Findings
1. Algorithmic bias is pervasive
2. Transparency is crucial
3. Regulation is needed
      ]]></content>
    </page>
  </pages>
  <links>
    <link from="research-question" to="literature" type="explores" />
    <link from="literature" to="findings" type="leads-to" />
  </links>
</nml>
```

### Personal Knowledge Base
```xml
<nml version="2.0">
  <meta title="Learning JavaScript" author="Student" />
  <pages>
    <page id="basics" x="0" y="0" color="blue">
      <content><![CDATA[
# JavaScript Basics
Variables, functions, objects, arrays...
      ]]></content>
    </page>
    <page id="async" x="300" y="0" color="yellow">
      <content><![CDATA[
# Async Programming  
Promises, async/await, callbacks...
      ]]></content>
    </page>
    <page id="frameworks" x="600" y="0" color="green">
      <content><![CDATA[
# Frameworks
React, Vue, Angular comparison...
      ]]></content>
    </page>
  </pages>
  <links>
    <link from="basics" to="async" type="leads-to" />
    <link from="async" to="frameworks" type="leads-to" />
  </links>
</nml>
```

## Specification

For complete technical details, see [SPECIFICATION.md](SPECIFICATION.md)

## Contributing

We welcome contributions to the NML format specification and ecosystem!

### Areas for Contribution
- Parser implementations in various languages
- Editor plugins and extensions
- Documentation improvements
- Example projects and templates
- Format specification enhancements

### Development Setup
```bash
git clone https://github.com/your-org/nml.git
cd nml
npm install
npm run validate-examples
npm test
```

### Submitting Changes
1. Fork the repository
2. Create a feature branch
3. Add tests for any changes
4. Update documentation
5. Submit a pull request

## Roadmap

### Version 2.1 (Planned)
- [ ] Improved validation rules
- [ ] Better error messages  
- [ ] Performance optimizations
- [ ] Additional connection types

### Version 3.0 (Future)
- [ ] Collaborative editing support
- [ ] Plugin architecture
- [ ] Advanced styling options
- [ ] Export format extensions

## Community

- **Discussions**: [GitHub Discussions](https://github.com/your-org/nml/discussions)
- **Issues**: [Bug reports and feature requests](https://github.com/your-org/nml/issues)
- **Discord**: [NML Community Server](https://discord.gg/nml-community)
- **Twitter**: [@NMLFormat](https://twitter.com/nmlformat)

## License

NML is released under the MIT License. See [LICENSE](LICENSE) for details.

The format specification is public domain to encourage adoption across tools and platforms.

---

**Build better knowledge, visually organized** 🚀

Made with ❤️ by the open source community