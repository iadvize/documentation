# JavaScript Web SDK

## Overview <span hidden>Web SDK</span>

The Web SDK is a way to interact with the iAdvize solution from the client side.

## Safely accessing the iAdvize object

If the iAdvize tag was installed using the recommended script (see https://ha.iadvize.com/admin/site/current/code), there should be a global `window.iAdvizeInterface` available. You can safely push functions inside `window.iAdvizeInterface` : they are guaranteed to be executed once the iAdvize tag is fully loaded. 

<pre class="prettyprint lang-js">
window.iAdvizeInterface.push(function(iAdvize) {
  // Ex : accessing the tag version
  const tagVersion = iAdvize.get('tag:version');
});
</pre>

## List of methods
| Method                   | Description                                                                                                |
|--------------------------|------------------------------------------------------------------------------------------------------------|
| activate                 | Activates the tag with an identity. Needed when authentication is enabled.                                 |
| get                      | Getters                                                                                                    |
| on / off                 | Event listeners                                                                                            |
| help                     | Displays a list of available commands in the console                                                       |
| logout                   | Removes an identity, effectively stopping the tag when authentication is enabled.                          |
| navigate                 | Changes the current screen and restart the tag, allowing a new targeting run                               |
| recordTransaction        | Records a transaction                                                                                      |
| set                      | Setters                                                                                                    |

## iAdvize.activate / iAdvize.logout
These methods are used for authentication. Please see the dedicated Help Center article : https://help.iadvize.com/hc/articles/6043078724626

## iAdvize.get

`iAdvize.get` takes a single property argument, and returns the associated value. Properties are keys that reference values that can change over time. These values can be accessed : 
- directly, using `iAdvize.get` (ex: `iAdvize.get('visitor:cookiesConsent')`)
- when they change, using iAdvize.on (ex: `iAdvize.on('visitor:cookiesConsentChange', callback)`)


| Property                         | Description                                            | Values                       |
|----------------------------------|--------------------------------------------------------|------------------------------|
| tag:version                      | The tag version                                        | `"LIGHT"`, `"FULL"`                   |
| visitor:cookiesConsent           | Whether the visitor consented to cookies or not        | `"true"`,  `"false"` , `"unknown"` (default) |
| visitor:GDPRConsent              | Whether the visitor consented to GDPR or not           | `"true"`,  `"false"` , `"unknown"` (default) |

Ex : 
<pre class="prettyprint lang-js">
window.iAdvizeInterface.push(function(iAdvize) {
  const visitorCookiesConsent = iAdvize.get('visitor:cookiesConsent');
});
</pre>


## iAdvize.on / iAdvize.off
`iAdvize.on` takes two arguments : 
- The name of an event,
- A callback that takes the associated event value as parameter.

Every property available on `iAdvize.get` also has a corresponding event (iAdvize.on('{property}Change', (value) => {...})).
`iAdvize.off` takes the same arguments to remove the event listener.

Ex : 
<pre class="prettyprint lang-js">
window.iAdvizeInterface.push(function(iAdvize) {
  iAdvize.on('visitor:cookiesConsent', function(visitorCookiesConsent) {
    console.log(visitorCookiesConsent);
  });
});
</pre>

## iAdvize.set
Set editable properties.

| Property                         | Description                                            | Values                       |
|----------------------------------|--------------------------------------------------------|------------------------------|
| visitor:cookiesConsent           | Whether the visitor consented to cookies or not        | `true`, `false` |
| visitor:GDPRConsent              | Whether the visitor consented to GDPR or not           | `true`, `false` |

Ex : 
<pre class="prettyprint lang-js">
window.iAdvizeInterface.push(function(iAdvize) {
  iAdvize.set('visitor:GDPRConsent', true);
});
</pre>

## iAdvize.help
- Lists all the available methods,
- Lists all the available properties on `get` and `set`,
- Lists all the available events on `on` and `off`. 

## iAdvize.recordTransaction
Allows to record transactions. See the dedicated article on the Help Center : https://help.iadvize.com/hc/en-gb/articles/206375538

Ex : 
<pre class="prettyprint lang-js">
window.iAdvizeInterface.push(function(iAdvize) {
  iAdvize.recordTransaction({
    id: 'unique-id',
    amount: 49.95,
  });
});
</pre>