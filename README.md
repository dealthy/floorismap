# Central Pennsylvania Rivers - Interactive Map

An interactive 3D map showcasing the Susquehanna and Juniata rivers with oblique perspective, terrain visualization, and historical town markers.

## Features

- **3D Terrain Visualization**: Enhanced topography with 1.5x exaggeration to showcase the river valleys
- **Oblique Perspective**: 60-degree pitch angle provides a dramatic view of the landscape
- **River Flow Animation**: Automated camera movement following the river downstream
- **Interactive Towns**: Clickable markers for historic communities along both rivers
- **Dual River Views**: Switch between Susquehanna and Juniata river perspectives
- **Responsive Design**: Works on desktop and mobile devices

## Setup Instructions

### 1. Get a Mapbox Access Token

1. Go to [https://account.mapbox.com/](https://account.mapbox.com/)
2. Sign up for a free account (or log in)
3. Navigate to "Access tokens" in your account dashboard
4. Click "Create a token" or copy your default public token
5. The free tier includes 50,000 map loads per month (plenty for most websites)

### 2. Configure the Map

Open `susquehanna-map.html` and find this line (around line 323):

```javascript
mapboxgl.accessToken = 'YOUR_MAPBOX_TOKEN';
```

Replace `'YOUR_MAPBOX_TOKEN'` with your actual token:

```javascript
mapboxgl.accessToken = 'pk.eyJ1IjoieW91cnVzZXJuYW1lIiwiYSI6ImFiYzEyM3h5eiJ9.example-token-here';
```

### 3. Test Locally

Simply open the `susquehanna-map.html` file in a web browser. The map should load with the default Susquehanna River view.

## WordPress Integration

### Option 1: Full Page Template (Recommended)

1. **Create a new page template:**
   - Go to your WordPress theme folder
   - Create a new file: `template-river-map.php`
   - Add this code:

```php
<?php
/*
Template Name: River Map
*/
?>
<!DOCTYPE html>
<html <?php language_attributes(); ?>>
<head>
    <meta charset="<?php bloginfo( 'charset' ); ?>">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title><?php wp_title(); ?></title>
    
    <!-- Mapbox GL JS -->
    <link href="https://api.mapbox.com/mapbox-gl-js/v3.0.1/mapbox-gl.css" rel="stylesheet">
    <script src="https://api.mapbox.com/mapbox-gl-js/v3.0.1/mapbox-gl.js"></script>
    <script src="https://cdn.jsdelivr.net/npm/@turf/turf@6/turf.min.js"></script>
    
    <!-- Paste the entire <style> section from susquehanna-map.html here -->
    
</head>
<body>
    <!-- Paste the entire <body> content from susquehanna-map.html here -->
    
    <?php wp_footer(); ?>
</body>
</html>
```

2. **Create a new page in WordPress:**
   - Go to Pages > Add New
   - Give it a title like "River Map"
   - In the Template dropdown, select "River Map"
   - Publish the page

### Option 2: Embed in Existing Page

1. **Upload the HTML file to your media library** or host it on your server

2. **Use an iframe in your WordPress page:**

```html
<iframe 
    src="/path-to-your-map/susquehanna-map.html" 
    style="width: 100%; height: 600px; border: none;"
    title="Central Pennsylvania Rivers Map">
</iframe>
```

### Option 3: Custom HTML Block

1. Edit a WordPress page
2. Add a "Custom HTML" block
3. Paste the entire content from `susquehanna-map.html`
4. Make sure your theme allows JavaScript in Custom HTML blocks

## Customization Guide

### Change River Data

Located in the `riverData` object (around line 327):

```javascript
const riverData = {
    susquehanna: {
        name: "Susquehanna River",
        center: [-76.884, 40.790], // [longitude, latitude]
        zoom: 9,
        bearing: -30, // Camera rotation
        pitch: 60,    // Camera tilt (0-85)
        waypoints: [  // Path coordinates
            [-76.783, 41.245],
            // Add more waypoints...
        ],
        towns: [      // Town markers
            { name: "Lock Haven", coords: [-77.447, 41.137] },
            // Add more towns...
        ]
    }
};
```

### Adjust Terrain Exaggeration

Find this line (around line 362):

```javascript
map.setTerrain({ 'source': 'mapbox-dem', 'exaggeration': 1.5 });
```

- Lower values (1.0-1.2): More realistic terrain
- Higher values (2.0-3.0): More dramatic mountains

### Change Map Style

Find this line (around line 348):

```javascript
style: 'mapbox://styles/mapbox/outdoors-v12',
```

Replace with:
- `'mapbox://styles/mapbox/satellite-v9'` - Satellite imagery
- `'mapbox://styles/mapbox/streets-v12'` - Street map
- `'mapbox://styles/mapbox/light-v11'` - Light theme
- `'mapbox://styles/mapbox/dark-v11'` - Dark theme

### Modify Colors

CSS variables are at the top of the `<style>` section (around line 24):

```css
:root {
    --primary-blue: #2563eb;
    --river-blue: #0ea5e9;
    --terrain-green: #16a34a;
    --earth-brown: #78350f;
    --accent-gold: #f59e0b;
}
```

## Browser Compatibility

- Chrome/Edge: Full support
- Firefox: Full support
- Safari: Full support (iOS 15.4+)
- Mobile: Optimized for touch interactions

## Performance Tips

1. **Limit waypoints**: More waypoints = smoother animation but more processing
2. **Reduce terrain exaggeration** on slower devices
3. **Consider lazy loading** if embedding multiple maps on one page
4. **Use lower zoom levels** for initial view on mobile

## Troubleshooting

### Map doesn't load
- Check browser console for errors (F12)
- Verify your Mapbox token is correct
- Ensure you have internet connection
- Check if token has expired

### Markers don't appear
- Verify coordinates are in [longitude, latitude] format (not lat, lng)
- Check if coordinates are within the map bounds
- Look for JavaScript errors in console

### Animation is choppy
- Reduce number of waypoints
- Increase `stepDuration` in the `followRiver()` function
- Lower terrain exaggeration
- Try a simpler map style

## Future Enhancements

Ideas for extending this map:

1. **Historical Overlays**: Add old maps as image overlays
2. **Story Points**: Create narrative waypoints with historical information
3. **Water Quality Data**: Integrate real-time environmental data
4. **Photo Gallery**: Link historic photos to specific locations
5. **Compare Mode**: Show before/after views of the region
6. **3D Buildings**: Add historic building models
7. **Flood Zones**: Overlay FEMA flood data
8. **Trail Systems**: Add hiking/biking trails along the rivers

## Resources

- [Mapbox GL JS Documentation](https://docs.mapbox.com/mapbox-gl-js/)
- [Mapbox Studio](https://studio.mapbox.com/) - Create custom map styles
- [Turf.js Documentation](https://turfjs.org/) - Geospatial analysis
- [Pennsylvania GIS Data](https://www.pasda.psu.edu/) - Additional geographic data

## Credits

Map data © Mapbox © OpenStreetMap
Terrain data © Mapbox

## License

This code is provided as-is for your use. Feel free to modify and adapt it for your needs.

## Support

For Mapbox-specific questions, visit [Mapbox Community](https://community.mapbox.com/)
