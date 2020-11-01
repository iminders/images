VERSION?=1.0.0

push:
	echo "$(DOCKER_PASSWORD)" | docker login -u $(DOCKER_USERNAME) --password-stdin
	docker push aiminders/go:$(VERSION)
	docker logout

build:
	docker build -f Dockerfile -t aiminders/go:$(VERSION) .
	make push

latest:
	VERSION=latest
	docker build -f Dockerfile -t aiminders/go:$(VERSION) .
	make push
