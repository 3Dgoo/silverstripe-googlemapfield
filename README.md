googlemapfield
==============
Lets you record a precise location using latitude/longitude fields to a DataObject.

Displays a map using the Google Maps API. The user may then choose where to place the marker; the landing coordinates are then saved.

You can also search for locations using the search box, which uses the Google Maps Geocoding API.

Supports SilverStripe 3.0

## Usage

### Minimal configuration

Given your DataObject uses the field names `Lat` and `Lng` for storing the latitude and longitude respectively then the
following is a minimal setup to have the map show in the CMS:

```php
class Store extends DataObject
{
    public static $db = array(
        'Title' => 'Varchar(255)',
        'Lat' => 'Varchar',
        'Lng' => 'Varchar',
    );
    
    public function getCMSFields() {
        $fields = parent::getCMSFiels();
        
        // add the map field
        $fields->addFieldToTab('Root.Main', new GoogleMapField(
            $this,
            'Location'
        ));
        
        // remove the lat / lng fields from the CMS
        $fields->removeFieldFromTab('Root.Main', 'Lat');
        $fields->removeFieldFromTab('Root.Main', 'Lng');
        
        return $fields;
    }
}
```