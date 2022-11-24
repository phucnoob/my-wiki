## Thymeleaf live reload with npm

> This is not a tutorial, just a note to remind myself.

__Ideas__:

- Using nodejs tools to watch template change then copy them to classpath.
- String Devtools will watch changes on classpath and send reload command to livereload extension
- Extension reload the browser.

1. Include spring dev tools to project
  ```xml
  <dependency>
      <groupId>org.springframework.boot</groupId>
      <artifactId>spring-boot-devtools</artifactId>
      <scope>runtime</scope>
      <optional>true</optional>
  </dependency>
  ```
2. Disable cache
```properties
spring.thymeleaf.cache=false
```

3. Init npm project and install a watcher
  ```js
  npm init -y
  npm i copy-and-watch --save-dev
  ```
4. Add watch script
  ```json
  {
    "name": "livereload",
    "version": "1.0.0",
    "description": "",
    "main": "index.js",
    "scripts": {
      "dev": "copy-and-watch --watch src/main/resources/templates/**html target/classes/templates/"
    },
    "keywords": [],
    "author": "",
    "license": "ISC",
    "devDependencies": {
      "copy-and-watch": "^0.1.6",
      "npm-run-all": "^4.1.5"
    }
  }
  ```
5. Run script
6. Install livereload-extension (Chrome LiveReload or something etc)

Enjoy!
