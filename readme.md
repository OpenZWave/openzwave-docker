# openzwave-docker

> Always up to date openzwave base image

- Updated nightly (thanks [@dependabot](.dependabot/config.yml))
- Cross architecture
- Support [centos8](./Dockerfile.centos8), [alpine](./Dockerfile.alpine), [debian](./Dockerfile.debian), [ubuntu](./Dockerfile.ubuntu)

## Available docker tags:

- `chrisns/openzwave:centos8`
- `chrisns/openzwave:debian`
- `chrisns/openzwave:ubuntu`
- `chrisns/openzwave:alpine`
- in addition there is also a copy of each suffixed with `-sha:....` with the git sha from [openzwave](https://github.com/openzwave/open-zwave)
- and also `-version` based on the tagged stable versions from [openzwave](http://old.openzwave.com/downloads/) e.g. `chrisns/openzwave:centos8-1.6.1210`

### Stable builds

Unfortunately stable builds aren't trackable by dependabot as best I can find, so new builds requiring managing the [workflow file](.github/workflows/dockerbuild.yml) pull requests very welcome if you see new versions before I do!

## Expected usage

It's not expected that you'll use this image on its own, you'll base your project off of it.

```Dockerfile
FROM chrisns/openzwave:alpine as build

FROM node:alpine

COPY --from=build /openzwave/libopenzwave.so* /lib/
COPY --from=build /openzwave/config /usr/local/etc/openzwave
COPY . /app

ENV LD_LIBRARY_PATH /lib

RUN npm i
CMD npm start
```
