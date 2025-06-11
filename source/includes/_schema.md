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

| Field Name | Type | Description | Required | PDF Support |
|------------|------|-------------|----------|-------------|
| `elementId` | `string` | Unique element identifier | Yes | ✓ |
| `elementName` | `string` | Element display name | Yes | ✓ |
| `elementType` | `string` | Element type | Yes | ✓ |
| `displayName` | `string` | English display name | No | ✓ |
| `layoutConfig` | `LayoutConfiguration` | Layout configuration | Yes | ✓ |
| `styleConfig` | `VisualStyle` or `PdfVisualStyle` | Style configuration | Yes | ✓ |
| `processingMeta` | `ProcessingMetadata` | Processing metadata | Yes | ✓ |
| `childElements` | `VisualElement[]` or `PdfVisualElement[]` | Child elements list | No | ✓ |
| `contentData` | `ElementContent` or `PdfElementContent` | Content data | No | ✓ |
| `componentSpec` | `ComponentDefinition` | Component specification | No | ✓ |
| `boundingBox` | `mixed` | **PDF-specific**: Element bounding box coordinates | No | PDF only |
| `displayOrder` | `number` | **PDF-specific**: Element display order | No | PDF only |

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
  "contentData": { /* Content data */ },
  "boundingBox": [0, 0, 100, 100],
  "displayOrder": 1
}
```

## Element Types

Supported UI element types in the schema:

### Type Values

| Type | Description | Usage | PDF Support |
|------|-------------|-------|-------------|
| `"Body"` → `"Container"` | Page or container root element | Main page structure | ✓ |
| `"Layer"` → `"Panel"` | Generic container for organizing elements | Layout containers | ✓ |
| `"Image"` → `"Picture"` | Image display element | Visual content | ✓ |
| `"Text"` → `"Label"` | Text display element | Textual content | ✓ |
| `"Component"` → `"Widget"` | Reusable custom component | Custom components | ✓ |
| `"Vector"` → `"Shape"` | **PDF-specific**: Vector graphics element | Vector drawings, shapes | PDF only |
| `"Group"` → `"Collection"` | **PDF-specific**: Grouped elements | Element collections | PDF only |

### Example
```json
{
  "elementType": "Panel",
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

| Field Name | Type | Description | Required | PDF Support |
|------------|------|-------------|----------|-------------|
| `widthSpec` | `Object` | Width specifications | Yes | ✓ |
| `heightSpec` | `Object` | Height specifications | Yes | ✓ |
| `textConfig` | `Object` | Text styling configuration | No | ✓ |
| `borderConfig` | `Object` | Border styling configuration | No | ✓ |
| `backgroundSpec` | `Object` | Background specifications | No | ✓ |
| `effectsList` | `Array` | Visual effects list | No | ✓ |
| `textColor` | `VisualColor` | Text color settings | No | ✓ |
| `paddingValues` | `mixed` | Padding values | No | ✓ |
| `opacityLevel` | `number` | Opacity level (0-255) | No | ✓ |
| `overflowMode` | `Array` | Overflow handling mode | No | ✓ |
| `rotationAngle` | `number` | Rotation angle in degrees | No | ✓ |
| `textDetection` | `Object` | Text detection metadata | No | ✓ |
| `textExtraction` | `Object` | Text extraction metadata | No | ✓ |

### PDF-Specific Style Fields

The following fields are available only in PDF processing scenarios:

| Field Name | Type | Description | Source Field |
|------------|------|-------------|--------------|
| `characterData` | `Object` | **PDF-specific**: Character-level styling data | `chars` |
| `transformMatrix` | `number[]` | **PDF-specific**: Transformation matrix | `transform` |
| `cornerRadius` | `number` | **PDF-specific**: Corner radius value | `radius` |
| `isRightToLeft` | `boolean` | **PDF-specific**: Right-to-left text direction | `arabic` |
| `extendedMatrix` | `string` | **PDF-specific**: Extended transformation matrix | `ex_transform` |

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

### PDF-Specific Style Example

```json
{
  "styleConfig": {
    "widthSpec": {"sizing": "FIXED", "value": 200},
    "heightSpec": {"sizing": "FIXED", "value": 100},
    "characterData": {
      "0": {"size": 12, "fontFamily": "Arial"},
      "1": {"size": 14, "fontFamily": "Bold"}
    },
    "transformMatrix": [1.0, 0.0, 0.0, 1.0, 50.0, 100.0],
    "cornerRadius": 5,
    "isRightToLeft": false,
    "extendedMatrix": "matrix(1,0,0,1,0,0)"
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

| Field Name | Type | Description | Applicable Elements | PDF Support |
|------------|------|-------------|-------------------|-------------|
| `textValue` | `string` | Text content | Text | ✓ |
| `imageSource` | `string` | Image URL source | Image | ✓ |
| `colorReference` | `string` | Color token reference | Any | ✓ |
| `componentReference` | `string` | Component reference ID | Component | ✓ |
| `componentAttributes` | `Object` | Component attributes | Component | ✓ |

### PDF-Specific Content Fields

The following content fields are available only in PDF processing scenarios:

| Field Name | Type | Description | Source Field | Applicable Elements |
|------------|------|-------------|--------------|-------------------|
| `vectorData` | `VectorData` | **PDF-specific**: Vector graphics data | `vector` | Vector/Shape |
| `maskingMode` | `string` | **PDF-specific**: Masking mode | `maskType` | Any |
| `blendingType` | `string` | **PDF-specific**: Blending mode | `blendMode` | Any |
| `svgTemplate` | `string` | **PDF-specific**: SVG template string | `svgTemplate` | Vector/Shape |
| `imageData` | `string` | **PDF-specific**: Base64 encoded image data | `imageBase64` | Image |

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
  "imageData": "data:image/png;base64,iVBORw0KGgoAAAANSUhEUgAAAAEAAAABCAYAAAAfFcSJ..."
}
```

#### PDF Vector Content
```json
{
  "vectorData": {
    "pathItems": [
      {
        "pathType": "l",
        "coordinates": [
          {"xPosition": 0, "yPosition": 0},
          {"xPosition": 100, "yPosition": 100}
        ]
      }
    ],
    "evenOddRule": false,
    "layerIndex": 1,
    "vectorType": "path",
    "strokeOpacity": 1.0,
    "strokeColor": {
      "rgbValues": [0, 123, 255],
      "hexCode": "#007bff"
    },
    "strokeWidth": 2.0,
    "lineCapStyle": "round",
    "lineJoinStyle": "round",
    "isClosedPath": false
  },
  "maskingMode": "normal",
  "blendingType": "multiply"
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

## PDF Vector Data Structure

**Note**: The following structures are specific to PDF processing scenarios.

### VectorData Structure

| Field Name | Type | Description | Source Field |
|------------|------|-------------|--------------|
| `pathItems` | `PathItem[]` | Array of path elements | `items` |
| `evenOddRule` | `boolean` | Even-odd fill rule | `even_odd` |
| `layerDepth` | `string` | Layer depth identifier | `level` |
| `layerIndex` | `number` | Layer index number | `layer` |
| `vectorType` | `string` | Vector type identifier | `type` |
| `strokeOpacity` | `number` | Stroke opacity (0.0-1.0) | `stroke_opacity` |
| `strokeColor` | `VisualColor` | Stroke color | `color` |
| `fillColor` | `VisualColor` | Fill color | `fill` |
| `fillOpacity` | `number` | Fill opacity (0.0-1.0) | `fill_opacity` |
| `lineCapStyle` | `string` | Line cap style | `lineCap` |
| `lineJoinStyle` | `string` | Line join style | `lineJoin` |
| `dashPattern` | `number[]` | Dash pattern array | `dashes` |
| `strokeWidth` | `number` | Stroke width | `lineWidth` |
| `isClosedPath` | `boolean` | Whether path is closed | `closePath` |

### PathItem Structure

| Field Name | Type | Description | Source Field |
|------------|------|-------------|--------------|
| `pathType` | `string` | Path type ("l" for line, "c" for curve) | `vector_type` |
| `coordinates` | `PositionData[]` | Array of position coordinates | `points` |

### PositionData Structure

| Field Name | Type | Description | Source Field |
|------------|------|-------------|--------------|
| `xPosition` | `number` | X coordinate | `x` |
| `yPosition` | `number` | Y coordinate | `y` |

### PDF Vector Example

```json
{
  "vectorData": {
    "pathItems": [
      {
        "pathType": "l",
        "coordinates": [
          {"xPosition": 50.0, "yPosition": 50.0},
          {"xPosition": 250.0, "yPosition": 50.0}
        ]
      },
      {
        "pathType": "c",
        "coordinates": [
          {"xPosition": 250.0, "yPosition": 50.0},
          {"xPosition": 275.0, "yPosition": 25.0},
          {"xPosition": 275.0, "yPosition": 75.0},
          {"xPosition": 250.0, "yPosition": 100.0}
        ]
      }
    ],
    "evenOddRule": false,
    "layerIndex": 1,
    "vectorType": "path",
    "strokeOpacity": 1.0,
    "strokeColor": {
      "rgbValues": [0, 123, 255],
      "hexCode": "#007bff"
    },
    "fillColor": {
      "rgbValues": [255, 255, 255],
      "hexCode": "#ffffff"
    },
    "fillOpacity": 0.5,
    "lineCapStyle": "round",
    "lineJoinStyle": "round",
    "dashPattern": [5, 3],
    "strokeWidth": 2.0,
    "isClosedPath": false
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

## Field Mapping Reference

### Standard to Masked Field Mappings

#### Basic Fields
| Original Field | Masked Field | Notes |
|----------------|--------------|-------|
| `id` | `elementId` | Element identifier |
| `name` | `elementName` | Element name |
| `type` | `elementType` | Element type (mapped) |
| `enName` | `displayName` | English display name |
| `children` | `childElements` | Child elements array |
| `layout` | `layoutConfig` | Layout configuration |
| `style` | `styleConfig` | Style configuration |
| `i2dExt` | `processingMeta` | Processing metadata |
| `content` | `contentData` | Content data |
| `component` | `componentSpec` | Component specification |

#### PDF-Specific Field Mappings
| Original Field | Masked Field | Context | Notes |
|----------------|--------------|---------|-------|
| `sortIndex` | `displayOrder` | Basic | Display order |
| `rectanglePoint` | `boundingBox` | Basic | Bounding box coordinates |
| `chars` | `characterData` | Style | Character-level styling |
| `transform` | `transformMatrix` | Style | Transformation matrix |
| `radius` | `cornerRadius` | Style | Corner radius |
| `arabic` | `isRightToLeft` | Style | Text direction |
| `ex_transform` | `extendedMatrix` | Style | Extended transformation |
| `vector` | `vectorData` | Content | Vector graphics data |
| `maskType` | `maskingMode` | Content | Masking mode |
| `blendMode` | `blendingType` | Content | Blending type |
| `svgTemplate` | `svgTemplate` | Content | SVG template |
| `imageBase64` | `imageData` | Content | Base64 image data |

#### Vector Data Field Mappings (PDF-Specific)
| Original Field | Masked Field | Notes |
|----------------|--------------|-------|
| `items` | `pathItems` | Path items array |
| `even_odd` | `evenOddRule` | Even-odd fill rule |
| `level` | `layerDepth` | Layer depth |
| `layer` | `layerIndex` | Layer index |
| `vector_type` | `pathType` | Path type |
| `points` | `coordinates` | Coordinates array |
| `x` | `xPosition` | X coordinate |
| `y` | `yPosition` | Y coordinate |
| `stroke_opacity` | `strokeOpacity` | Stroke opacity |
| `fill_opacity` | `fillOpacity` | Fill opacity |
| `lineCap` | `lineCapStyle` | Line cap style |
| `lineJoin` | `lineJoinStyle` | Line join style |
| `dashes` | `dashPattern` | Dash pattern |
| `lineWidth` | `strokeWidth` | Stroke width |
| `closePath` | `isClosedPath` | Path closure flag |

#### Element Type Mappings
| Original Type | Masked Type | Context |
|---------------|-------------|---------|
| `Body` | `Container` | All |
| `Layer` | `Panel` | All |
| `Image` | `Picture` | All |
| `Text` | `Label` | All |
| `Component` | `Widget` | All |
| `Vector` | `Shape` | PDF-specific |
| `Group` | `Collection` | PDF-specific |

## Complete Example

### PDF Document Structure Example
```json
{
  "visualElement": {
    "elementId": "pdf_page_1",
    "elementName": "PDF Document Page",
    "elementType": "Panel",
    "displayName": "First Page",
    "displayOrder": 0,
    "boundingBox": [0, 0, 595, 842],
    "layoutConfig": {
      "positionMode": "Normal",
      "flexibleMode": "Absolute"
    },
    "styleConfig": {
      "widthSpec": {"sizing": "FIXED", "value": 595},
      "heightSpec": {"sizing": "FIXED", "value": 842},
      "backgroundSpec": {
        "type": "COLOR",
        "backgroundColor": {"rgbValues": [255, 255, 255]}
      }
    },
    "processingMeta": {
      "surfaceArea": 501490,
      "detectionScore": 0.92,
      "textContainerized": false
    },
    "childElements": [
      {
        "elementId": "vector_diagram",
        "elementName": "Process Diagram",
        "elementType": "Shape",
        "displayOrder": 1,
        "layoutConfig": {
          "positionMode": "Absolute",
          "absoluteAttrs": {
            "align": ["LEFT", "TOP"],
            "coord": [50, 100]
          }
        },
        "styleConfig": {
          "widthSpec": {"sizing": "FIXED", "value": 300},
          "heightSpec": {"sizing": "FIXED", "value": 200}
        },
        "processingMeta": {
          "surfaceArea": 60000,
          "detectionScore": 0.89,
          "textContainerized": false
        },
        "contentData": {
          "vectorData": {
            "pathItems": [
              {
                "pathType": "l",
                "coordinates": [
                  {"xPosition": 50.0, "yPosition": 50.0},
                  {"xPosition": 250.0, "yPosition": 50.0}
                ]
              }
            ],
            "evenOddRule": false,
            "layerIndex": 1,
            "vectorType": "path",
            "strokeOpacity": 1.0,
            "strokeColor": {
              "rgbValues": [0, 123, 255],
              "hexCode": "#007bff"
            },
            "strokeWidth": 2.0,
            "lineCapStyle": "round",
            "lineJoinStyle": "round",
            "isClosedPath": false
          }
        }
      }
    ]
  },
  "configuration": {
    "baseWidth": 595,
    "measurementUnit": "pt",
    "scalingFactor": 1
  }
}
```
