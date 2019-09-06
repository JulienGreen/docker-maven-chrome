# markhobson/maven-chrome

Docker image for Java automated UI tests.

Includes:

* JDK 8/11/12
* Maven 3.6.1
* Chrome (latest)
* ChromeDriver 76

Available on [Docker Hub](https://hub.docker.com/r/markhobson/maven-chrome/).

## Tags

The following Docker tags are available:

* `latest` [(jdk-8/Dockerfile)](jdk-8/Dockerfile)
* `jdk-11` [(jdk-11/Dockerfile)](jdk-11/Dockerfile)
* `jdk-12` [(jdk-12/Dockerfile)](jdk-12/Dockerfile)

See issue [#11](https://github.com/markhobson/docker-maven-chrome/issues/11) to improve these tags.

## Demo

See the [demo](demo) Maven project to see how this Docker image can be used to run UI tests. The [run.sh](demo/run.sh) script builds the project within the latest version of this image on Docker Hub.

## Tips

### Configure Protractor to use bundled ChromeDriver

Set [`chromeDriver`](https://github.com/angular/protractor/blob/master/lib/config.ts#L76) in the Protractor conf.js file:

```js
exports.config = {
  chromeDriver: '/usr/bin/chromedriver'
}
```

### Chrome crashes

Chrome uses `/dev/shm` for runtime data which is 64MB by default under Docker. If this is not sufficient then this can cause [Chrome to crash](https://bugs.chromium.org/p/chromium/issues/detail?id=522853). Fix by either:

* Increase the size of `/dev/shm` (or mount it to the host's)
* Start Chrome with the flag `--disable-dev-shm-usage`
