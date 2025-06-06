# The Schema Object

## Overview

The Visual Element Schema is a comprehensive data structure for describing user interface elements and their properties. This schema provides a standardized approach to represent UI components, their layout configurations, styling properties, and content definitions.

## Root Structure

```json
{
  "visualElement": {
    // Main UI structure definition
  },
  "configuration": {
    // Global configuration options
  }
}
```

### Top-Level Fields

| Field Name | Type | Description | Required |
|------------|------|-------------|----------|
| `visualElement` | `VisualElement` | Main UI structure definition | Yes |
| `configuration` | `Configuration` | Global configuration options | No |

## VisualElement Structure

The `VisualElement` is the core data structure describing a single UI element and its properties.

### Basic Fields

| Field Name | Type | Description | Required |
|------------|------|-------------|----------|
| `elementId` | `string` | Unique element identifier | Yes |
| `elementName` | `string` | Element display name | Yes |
| `elementType` | `string` | Element type | Yes |
| `displayName` | `string` | English display name | No |
| `layoutConfig` | `LayoutConfiguration` | Layout configuration | Yes |
| `styleConfig` | `VisualStyle` | Style configuration | Yes |
| `processingMeta` | `ProcessingMetadata` | Processing metadata | Yes |
| `childElements` | `VisualElement[]` | Child elements list | No |
| `contentData` | `ElementContent` | Content data | No |
| `componentSpec` | `ComponentDefinition` | Component specification | No |

### Example Structure
```json
{
  "elementId": "element_001",
  "elementName": "Main Container",
  "elementType": "Body",
  "displayName": "Primary Layout Container",
  "layoutConfig": { /* Layout configuration */ },
  "styleConfig": { /* Style configuration */ },
  "processingMeta": { /* Processing metadata */ },
  "childElements": [ /* Child elements */ ],
  "contentData": { /* Content data */ }
}
```

## Element Types

Supported UI element types in the schema:

### Type Values

| Type | Description | Usage |
|------|-------------|-------|
| `"Body"` | Page or container root element | Main page structure |
| `"Layer"` | Generic container for organizing elements | Layout containers |
| `"Image"` | Image display element | Visual content |
| `"Text"` | Text display element | Textual content |
| `"Component"` | Reusable custom component | Custom components |

### Example
```json
{
  "elementType": "Layer",
  "elementName": "Header Section",
  "displayName": "Top Navigation Area"
}
```

## Layout Configuration

The `LayoutConfiguration` controls element positioning and layout behavior.

### Field Structure

| Field Name | Type | Description | Required |
|------------|------|-------------|----------|
| `positionMode` | `string` | Positioning mode | Yes |
| `flexibleMode` | `string` | Flexible layout type | No |
| `flexAttributes` | `Object` | Flexible layout attributes | No |
| `absoluteAttrs` | `Object` | Absolute positioning attributes | No |

### Position Modes

- **`"Normal"`**: Standard document flow
- **`"Absolute"`**: Absolute positioning
- **`"Relative"`**: Relative positioning
- **`"Flex"`**: Flexible box layout

### Flex Attributes Example
```json
{
  "flexAttributes": {
    "alignItems": "center",
    "justifyContent": "space-between",
    "flexDirection": "column",
    "flexWrap": "nowrap"
  }
}
```

### Absolute Positioning Example
```json
{
  "absoluteAttrs": {
    "align": ["LEFT", "TOP"],
    "coord": [0, 0],
    "orginCoord": [0, 0]
  }
}
```

## Visual Style Configuration

The `VisualStyle` defines visual styling properties for elements.

### Main Style Fields

| Field Name | Type | Description | Required |
|------------|------|-------------|----------|
| `widthSpec` | `Object` | Width specifications | Yes |
| `heightSpec` | `Object` | Height specifications | Yes |
| `textConfig` | `Object` | Text styling configuration | No |
| `borderConfig` | `Object` | Border styling configuration | No |
| `backgroundSpec` | `Object` | Background specifications | No |
| `effectsList` | `Array` | Visual effects list | No |
| `textColor` | `VisualColor` | Text color settings | No |
| `paddingValues` | `mixed` | Padding values | No |
| `opacityLevel` | `number` | Opacity level (0-255) | No |
| `overflowMode` | `Array` | Overflow handling mode | No |
| `rotationAngle` | `number` | Rotation angle in degrees | No |
| `textDetection` | `Object` | Text detection metadata | No |
| `textExtraction` | `Object` | Text extraction metadata | No |

### Size Configuration

```json
{
  "widthSpec": {
    "sizing": "FIXED",    // FIXED, FILL, FIT_CONTENT
    "value": 100
  },
  "heightSpec": {
    "sizing": "FILL",
    "value": 200
  }
}
```

### Text Configuration

```json
{
  "textConfig": {
    "fontSize": 16,
    "fontStyle": "normal",        // normal, bold, italic, semi_bold
    "textAlign": ["LEFT", "CENTER"],
    "fontFamily": "Arial",
    "lineHeight": 1.5,
    "letterSpacing": 0
  }
}
```

### Border Configuration

```json
{
  "borderConfig": {
    "borderWidth": 2,
    "borderStyle": "solid",
    "borderColor": {
      "rgbValues": [128, 128, 128],
      "hexCode": "#808080"
    },
    "borderRadius": [10, 10, 10, 10]
  }
}
```

### Background Specifications

#### Solid Color Background
```json
{
  "backgroundSpec": {
    "type": "COLOR",
    "backgroundColor": {
      "rgbValues": [255, 255, 255],
      "hexCode": "#ffffff"
    }
  }
}
```

#### Image Background
```json
{
  "backgroundSpec": {
    "type": "IMAGE",
    "imageUrl": "https://example.com/bg.jpg",
    "backgroundSize": "cover",
    "backgroundPosition": "center",
    "backgroundRepeat": "no-repeat"
  }
}
```

#### Gradient Background
```json
{
  "backgroundSpec": {
    "type": "LINEAR_GRADIENT",
    "deg": 45,
    "gradientStops": [
      {"color": {"rgbValues": [255, 0, 0]}, "position": 0},
      {"color": {"rgbValues": [0, 0, 255]}, "position": 100}
    ]
  }
}
```

## Color Definition

The `VisualColor` structure supports multiple color representation formats.

### Color Fields

| Field Name | Type | Description | Example |
|------------|------|-------------|---------|
| `rgbValues` | `number[]` | RGB values array | `[255, 128, 0]` |
| `hexCode` | `string` | Hexadecimal color code | `"#ff8000"` |

### Example
```json
{
  "rgbValues": [255, 128, 0],
  "hexCode": "#ff8000"
}
```

## Element Content

The `ElementContent` defines the actual content of elements.

### Content Fields

| Field Name | Type | Description | Applicable Elements |
|------------|------|-------------|-------------------|
| `textValue` | `string` | Text content | Text |
| `imageSource` | `string` | Image URL source | Image |
| `colorReference` | `string` | Color token reference | Any |
| `componentReference` | `string` | Component reference ID | Component |
| `componentAttributes` | `Object` | Component attributes | Component |

### Content Examples

#### Text Content
```json
{
  "textValue": "Welcome to our platform",
  "colorReference": "primary_text_color"
}
```

#### Image Content
```json
{
  "imageSource": "https://example.com/hero-image.jpg",
  "colorReference": null
}
```

#### Component Content
```json
{
  "componentReference": "button_primary",
  "componentAttributes": {
    "variant": {"type": "primary"},
    "size": {"value": "large"},
    "action": {"handler": "submitForm"}
  }
}
```

## Component Definition

The `ComponentDefinition` structure for reusable components.

### Component Fields

| Field Name | Type | Description |
|------------|------|-------------|
| `componentId` | `string` | Component identifier |
| `componentName` | `string` | Component display name |
| `sourceCode` | `string` | Component implementation code |
| `configOptions` | `Object` | Configuration options schema |

### Example
```json
{
  "componentId": "interactive_button",
  "componentName": "Interactive Button Component",
  "sourceCode": "/* React component implementation */",
  "configOptions": {
    "variant": "string",
    "size": "string",
    "disabled": "boolean",
    "onClick": "function"
  }
}
```

## Processing Metadata

The `ProcessingMetadata` contains technical processing information.

### Metadata Fields

| Field Name | Type | Description |
|------------|------|-------------|
| `surfaceArea` | `number` | Element surface area in pixels |
| `detectionScore` | `number` | Detection confidence score (0.0-1.0) |
| `textContainerized` | `boolean` | Whether text is containerized |

### Example
```json
{
  "surfaceArea": 960000,
  "detectionScore": 0.95,
  "textContainerized": true
}
```

## Global Configuration

The `Configuration` object contains global settings.

### Configuration Fields

| Field Name | Type | Description | Default |
|------------|------|-------------|---------|
| `baseWidth` | `number` | Base design width | 375 |
| `measurementUnit` | `string` | Measurement unit | "px" |
| `scalingFactor` | `number` | Scaling factor | 1 |

### Example
```json
{
  "baseWidth": 782,
  "measurementUnit": "px",
  "scalingFactor": 1
}
```

## Complete Example

### Full Structure Example
```json
{
  "visualElement": {
    "elementId": "main_page",
    "elementName": "Application Main Page",
    "elementType": "Body",
    "displayName": "Primary Application Interface",
    "layoutConfig": {
      "positionMode": "Normal",
      "flexibleMode": "Absolute"
    },
    "styleConfig": {
      "widthSpec": {"sizing": "FILL", "value": 782},
      "heightSpec": {"sizing": "FILL", "value": 1032},
      "backgroundSpec": {
        "type": "COLOR",
        "backgroundColor": {"rgbValues": [255, 255, 255]}
      }
    },
    "processingMeta": {
      "surfaceArea": 807024,
      "detectionScore": 0.0,
      "textContainerized": false
    },
    "childElements": [
      {
        "elementId": "header_container",
        "elementName": "Header Section",
        "elementType": "Layer",
        "layoutConfig": {
          "positionMode": "Absolute",
          "absoluteAttrs": {
            "align": ["LEFT", "TOP"],
            "coord": [0, 0]
          }
        },
        "styleConfig": {
          "widthSpec": {"sizing": "FILL", "value": 782},
          "heightSpec": {"sizing": "FIXED", "value": 120}
        },
        "processingMeta": {
          "surfaceArea": 93840,
          "detectionScore": 0.9,
          "textContainerized": false
        },
        "childElements": [
          {
            "elementId": "page_title",
            "elementName": "Page Title Text",
            "elementType": "Text",
            "layoutConfig": {
              "positionMode": "Absolute",
              "absoluteAttrs": {
                "align": ["CENTER", "CENTER"],
                "coord": [391, 60]
              }
            },
            "styleConfig": {
              "widthSpec": {"sizing": "FIT_CONTENT", "value": 200},
              "heightSpec": {"sizing": "FIT_CONTENT", "value": 40},
              "textConfig": {
                "fontSize": 24,
                "fontStyle": "bold",
                "textAlign": ["CENTER", "CENTER"],
                "fontFamily": "Inter"
              },
              "textColor": {"rgbValues": [33, 33, 33]}
            },
            "processingMeta": {
              "surfaceArea": 8000,
              "detectionScore": 0.95,
              "textContainerized": false
            },
            "contentData": {
              "textValue": "Welcome to Main Page"
            }
          }
        ]
      }
    ]
  },
  "configuration": {
    "baseWidth": 782,
    "measurementUnit": "px",
    "scalingFactor": 1
  }
}
```
