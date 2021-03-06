## Working with Javascript manager

The Javascript manager allow you to generate file path directly in Javascript.

### Installation

Register the bundle in `app/AppKernel.php`:

```php
// app/AppKernel.php
public function registerBundles()
{
    return array(
        // ...
        new \Novaway\Bundle\FileManagementBundle\NovawayFileManagementBundle(),
    );
}
```

Register the routing definition in `app/config/routing.yml`:

```yml
# app/config/routing.yml
novaway_file_management:
    resource: "@NovawayFileManagementBundle/Controller/"
    type:     annotation
    prefix:   /
```

Publish assets:

    $ php app/console assets:install --symlink web

### Usage

Include the file in your layout:

```html
<script src="{{ asset('bundles/novawayfilemanagement/js/filemanager.js') }}"></script>
```

**Note:** if you are not using Twig, that's not a problem. What you need is to
load the JavaScript file above somewhere in your web page.

Then you can create your manager:

```javascript
var manager = new FileManager('webpath', {
    photo: ['original', 'thumb']
});
```

And use it to generate image path:

```javascript
manager.getPath(mediaJsonEntity, 'photo', 'original')
```

### Usage with manager is declared as a service

If your manager is declared as a service, you can create a javascript manager using twig :

```html
<script type="text/javascript" src="{{ path('novaway_filemanagement_routing_js', { service_manager: 'your_service.id', manager: 'myManager' }) }}"></script>
```

or

```
{{ render(url('novaway_filemanagement_routing_js', { service_manager: 'your_service.id', manager: 'myManager' })) }}
```

Which is the equivalent of :

```javascript
var myManager = new novaway.FileManager();
myManager.setData({/* json data */});
```
