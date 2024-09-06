# Building multi-stage images

## Scenario 1

```
cd scenario-01 && docker build -t docker-stages:1 .
docker run -it docker-stages:1 /bin/sh
```

## Scenario 2

```
cd ../scenario-02 && docker build -t docker-stages:2 .
docker run -it docker-stages:2 /bin/sh
```

## Scenario 3

```
cd ../scenario-03 && docker build -t docker-stages:3 .
docker run -it docker-stages:3 /bin/sh
```

## Scenario 4

```
cd ../scenario-04 && docker build -t docker-stages:4 .
docker run -it docker-stages:4
docker run -it docker-stages:4 /bin/sh
```

## Scenario 5

Set a target stage

```
cd ../scenario-05 && docker build --target dev -t docker-stages:5 .
docker run -v ./src:/app/src docker-stages:5
docker run -it docker-stages:5 /bin/sh
```
