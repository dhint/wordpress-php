-include env_make

VERSION ?= 7.1

REPO = wodby/wordpress-php
NAME = wordpress-php-$(VERSION)

.PHONY: build test push shell run start stop logs clean release

build:
	docker build -t $(REPO):$(VERSION) ./

test:
	docker build -t $(REPO)-test:$(VERSION) ./test
	docker run --rm --name $(NAME)-test $(REPO)-test:$(VERSION)

push:
	docker push $(REPO):$(VERSION)

shell:
	docker run --rm --name $(NAME) -i -t $(PORTS) $(VOLUMES) $(ENV) $(REPO):$(VERSION) /bin/bash

run:
	docker run --rm --name $(NAME) $(PORTS) $(VOLUMES) $(ENV) $(REPO):$(VERSION) $(CMD)

start:
	docker run -d --name $(NAME) $(PORTS) $(VOLUMES) $(ENV) $(REPO):$(VERSION)

stop:
	docker stop $(NAME)

logs:
	docker logs $(NAME)

clean:
	-docker rm -f $(NAME)
	-docker rm -f $(NAME)-test

release: build
	make push -e VERSION=$(VERSION)

default: build
