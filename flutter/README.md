[toc]

# Flutter memorendum



## Utilities


### Libraries

Good libraries I have used

- Documents handling => PDF



```yaml
dependencies:
  # ...
  
  # window sizing for Flutter Desktop
  desktop_window: ^0.4.0

  # For mysql connexion support.
  dart_mysql: ^0.0.1
  # mysql1: ^0.19.2  # alternativ mysql client

  # standardized logs
  logging: ^1.0.2

  # streambuilder
  provider: ^5.0.0
  
  # helper for state management and comparison of objets/entities
  equatable: ^2.0.3

  # IO helper
  path: ^1.8.0

  # printing to PDF
  pdf: ^3.8.1
  printing: ^5.9.1

  # screenshots
  screenshot: ^1.2.3
```





## Tricks



- [Add firefox as device when running flutter web](https://stackoverflow.com/questions/71517888/add-firefox-as-device-when-running-flutter-web)


You can run the project with web-server as the device :

`flutter run -d web-server`

Then you can open the url where lib/main.dart is served (it is shown on console), from the browser of your choice (e.g Firefox).




----

- [How can I run flutter web app without internet connection](https://stackoverflow.com/questions/73109896/how-can-i-run-flutter-web-app-without-internet-connection)

> I created a flutter web application, and I finished building it with the command .. flutter build web --release , and then transferred it to a local server , The site does not work unless it is connected to the Internet...



The problem is, that flutter has some dependencies, that can not be  resolved when you, as the client, are offline. Mostly consisting of `canvaskit` and certain google fonts.

There are multiple solutions for that. The easiest being to use the html web-renderer:

```bash
flutter build web --release --web-renderer html
```

this should work for most applications, however it has lower performance than `canvaskit`, especially with high widget density.

Therefore you can also use `canvaskit` locally as it is  automatically built when you build your release. But you have to set it  as base url, by adding the following lines in your index.html:

```html
<script>
  window.flutterConfiguration = {
      canvasKitBaseUrl: "/canvaskit/"
  };
</script>
```

This makes sure your flutter application uses the local source for `canvaskit`. However, another problem could be the usage of google fonts, e.g.  Roboto, as those often need to be downloaded as well. But you can just  add those to the `pubspec.yaml` explicitly to account for that, like explained [here](https://docs.flutter.dev/cookbook/design/fonts).

Some sources for more informations:

[flutter web-renderers](https://docs.flutter.dev/development/platform-integration/web/renderers)

[The same issue but on github](https://github.com/flutter/flutter/issues/78235)

[Making Flutter offline capable](https://github.com/flutter/flutter/issues/60069)



----





## **Lessons**



