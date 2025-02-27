# Convert ESRI styles to OpenLayers styles

## Info

This module can convert ESRI style definition to OpenLayers style function. ESRI style definition must be in JSON format - [https://developers.arcgis.com/documentation/common-data-types/renderer-objects.htm][arcgis-docs]

## Getting started

Import as ES6 module:

```javascript
import { createStyleFunctionFromUrl } from 'ol-esri-style';

// create a new vector layer
const vector = new VectorLayer({
  ...
});


// set layer style
// Passing the projection is need for labeling features. Visible resolutions for
// the labels are calculated using map projection units.
createStyleFunctionFromUrl('arcgis_server_layer_url', map.getView().getProjection()).then(styleFunction => {
  vector.setStyle(styleFunction);
});
```

You can modify the styles before applying them to the features:
```javascript
// set layer style
createStyleFunctionFromUrl('arcgis_server_layer_url').then(styleFunction => {
  vector.setStyle((feature, resolution) => {
    const styles = styleFunction(feature, resolution);

    // modify styles

    return styles;
  });
});
```

## Example

To check the example stored in `/example` directory run:

```bash
npm run dev
```

The example loads data from [https://sampleserver3.arcgisonline.com/ArcGIS/rest/services/Petroleum/KSFields/FeatureServer/0][link-test-data] and the style definition is from [https://sampleserver3.arcgisonline.com/ArcGIS/rest/services/Petroleum/KSFields/FeatureServer/0?f=json][link-test-style].

## Dependencies

- [ol][link-npm-ol]
- [parcel][parcel-url]

## License

The MIT License (MIT).

[link-npm-ol]: https://www.npmjs.com/package/ol
[parcel-url]: https://parceljs.org
[arcgis-docs]: https://developers.arcgis.com/documentation/common-data-types/renderer-objects.htm
[link-test-style]: https://sampleserver3.arcgisonline.com/ArcGIS/rest/services/Petroleum/KSFields/FeatureServer/0?f=json
[link-test-data]: https://sampleserver3.arcgisonline.com/ArcGIS/rest/services/Petroleum/KSFields/FeatureServer/0
