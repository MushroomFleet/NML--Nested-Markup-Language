# NML (Nested Markdown Language) Specification v1.0

## Overview

NML is an XML-based format designed for storing interconnected markdown content on infinite canvases. It supports node-based linking, positioning, and rich metadata while maintaining markdown's simplicity within structured containers.

## Core Structure

### Document Root
```xml
<nml version="1.0" xmlns="http://nml.spec/2025">
  <metadata>
    <!-- Document-level metadata -->
  </metadata>
  <canvas>
    <!-- Canvas configuration -->
  </canvas>
  <nodes>
    <!-- All content nodes -->
  </nodes>
  <connections>
    <!-- Inter-node relationships -->
  </connections>
</nml>
```

## Elements Reference

### Document Metadata
```xml
<metadata>
  <title>My Knowledge Graph</title>
  <author>John Doe</author>
  <created>2025-01-15T10:30:00Z</created>
  <modified>2025-01-16T14:22:00Z</modified>
  <description>A collection of interconnected research notes</description>
  <tags>
    <tag>research</tag>
    <tag>ai</tag>
    <tag>knowledge-management</tag>
  </tags>
</metadata>
```

### Canvas Configuration
```xml
<canvas>
  <dimensions width="infinite" height="infinite" />
  <viewport x="0" y="0" zoom="1.0" />
  <grid enabled="true" size="20" opacity="0.1" />
  <theme>dark</theme>
</canvas>
```

### Content Nodes
```xml
<node id="unique-id" type="markdown|image|embed|group">
  <position x="100" y="200" z="0" />
  <size width="300" height="400" />
  <style>
    <background-color>#ffffff</background-color>
    <border-color>#cccccc</border-color>
    <border-width>1</border-width>
    <border-radius>8</border-radius>
    <opacity>1.0</opacity>
  </style>
  <metadata>
    <title>Node Title</title>
    <created>2025-01-15T10:30:00Z</created>
    <modified>2025-01-16T14:22:00Z</modified>
    <tags>
      <tag>important</tag>
      <tag>draft</tag>
    </tags>
  </metadata>
  <content type="markdown" encoding="utf-8">
    <![CDATA[
# This is a Markdown Header

This content supports **full markdown** including:

- Lists
- Links: [Example](https://example.com)
- Code blocks:

```javascript
const example = "Hello NML!";
```

> Blockquotes work too!

## Nested Content
You can reference other nodes using: [[node:another-node-id]]
    ]]>
  </content>
  <inputs>
    <input id="input-1" label="Main Input" x="0" y="50" />
    <input id="input-2" label="Secondary" x="0" y="100" />
  </inputs>
  <outputs>
    <output id="output-1" label="Result" x="300" y="50" />
    <output id="output-2" label="Alternative" x="300" y="100" />
  </outputs>
</node>
```

### Node Types

#### Markdown Node
```xml
<node id="md-001" type="markdown">
  <content type="markdown">
    <![CDATA[# Research Notes on AI Ethics...]]>
  </content>
</node>
```

#### Image Node
```xml
<node id="img-001" type="image">
  <content type="image" src="./images/diagram.png" alt="System Architecture" />
</node>
```

#### Embed Node
```xml
<node id="embed-001" type="embed">
  <content type="embed" src="https://youtube.com/watch?v=..." provider="youtube" />
</node>
```

#### Group Node
```xml
<node id="group-001" type="group">
  <members>
    <member node-id="md-001" />
    <member node-id="md-002" />
  </members>
  <content type="markdown">
    <![CDATA[# Group: Related Concepts]]>
  </content>
</node>
```

### Connections
```xml
<connections>
  <connection id="conn-001">
    <from node-id="node-1" output-id="output-1" />
    <to node-id="node-2" input-id="input-1" />
    <style>
      <line-color>#007acc</line-color>
      <line-width>2</line-width>
      <line-style>solid|dashed|dotted</line-style>
      <arrow-style>none|arrow|circle</arrow-style>
    </style>
    <metadata>
      <label>Influences</label>
      <type>causal|reference|hierarchy|sequence</type>
      <weight>1.0</weight>
    </metadata>
  </connection>
</connections>
```

## Advanced Features

### Cross-References
Within markdown content, reference other nodes:
```markdown
This concept builds on [[node:fundamental-concepts]] and leads to [[node:advanced-applications]].
```

### Conditional Content
```xml
<content type="markdown" conditions="tag:published">
  <![CDATA[This content only shows when the node has the 'published' tag.]]>
</content>
```

### Templates
```xml
<templates>
  <template id="research-note">
    <node type="markdown">
      <style>
        <background-color>#f8f9fa</background-color>
        <border-color>#007acc</border-color>
      </style>
      <content type="markdown">
        <![CDATA[
# Research Note Template

**Date:** {{created}}
**Tags:** {{tags}}

## Summary


## Details


## Related Work
- [[node:]]

## Next Steps

        ]]>
      </content>
    </node>
  </template>
</templates>
```

### Layers and Grouping
```xml
<layers>
  <layer id="background" z-index="-1" visible="true" locked="false" />
  <layer id="content" z-index="0" visible="true" locked="false" />
  <layer id="annotations" z-index="1" visible="true" locked="false" />
</layers>
```

## Example Complete Document

```xml
<?xml version="1.0" encoding="UTF-8"?>
<nml version="1.0" xmlns="http://nml.spec/2025">
  <metadata>
    <title>AI Research Canvas</title>
    <author>Research Team</author>
    <created>2025-01-15T10:30:00Z</created>
    <modified>2025-01-16T14:22:00Z</modified>
  </metadata>
  
  <canvas>
    <dimensions width="infinite" height="infinite" />
    <viewport x="0" y="0" zoom="1.0" />
  </canvas>
  
  <nodes>
    <node id="intro" type="markdown">
      <position x="100" y="100" />
      <size width="300" height="200" />
      <content type="markdown">
        <![CDATA[
# Introduction to AI Ethics

This is our starting point for exploring ethical considerations in AI development.

Key areas to explore:
- [[node:bias]] - Algorithmic bias
- [[node:privacy]] - Data privacy concerns
- [[node:transparency]] - AI explainability
        ]]>
      </content>
      <outputs>
        <output id="out1" label="Leads to" x="300" y="100" />
      </outputs>
    </node>
    
    <node id="bias" type="markdown">
      <position x="500" y="50" />
      <size width="300" height="250" />
      <content type="markdown">
        <![CDATA[
# Algorithmic Bias

Bias in AI systems can perpetuate and amplify existing societal inequalities.

## Types of Bias
- **Historical bias**: Training data reflects past discrimination
- **Representation bias**: Underrepresentation of certain groups
- **Measurement bias**: Different quality of data across groups

## Mitigation Strategies
- Diverse training datasets
- Regular bias audits
- Inclusive design processes
        ]]>
      </content>
      <inputs>
        <input id="in1" label="From intro" x="0" y="100" />
      </inputs>
    </node>
  </nodes>
  
  <connections>
    <connection id="intro-to-bias">
      <from node-id="intro" output-id="out1" />
      <to node-id="bias" input-id="in1" />
      <style>
        <line-color>#007acc</line-color>
        <line-width>2</line-width>
        <arrow-style>arrow</arrow-style>
      </style>
      <metadata>
        <type>reference</type>
        <label>explores</label>
      </metadata>
    </connection>
  </connections>
</nml>
```

## Implementation Notes

1. **Markdown Processing**: Content within `<![CDATA[]]>` blocks should be processed as standard CommonMark
2. **Node References**: `[[node:id]]` syntax should be resolved to actual connections or hyperlinks
3. **Positioning**: Coordinates are in canvas units (could be pixels, or abstract units)
4. **Validation**: XSD schema can be created for validation
5. **Extensions**: Custom node types and attributes can be added via namespaces

## File Extensions
- `.nml` - Standard NML files
- `.nmlx` - Compressed NML (ZIP containing NML + assets)

This format provides a robust foundation for infinite canvas applications while maintaining the simplicity that makes markdown so popular.