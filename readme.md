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
