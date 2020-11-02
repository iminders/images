# VERSION?=latest
# 20201102
VERSION?=1.15.0

push:
	echo "$(DOCKER_PASSWORD)" | docker login -u $(DOCKER_USERNAME) --password-stdin
	docker push aiminders/go:$(VERSION)
	docker image tag aiminders/go:$(VERSION) aiminders/go:latest
	docker push aiminders/go:latest
	docker logout

build:
	docker build -f Dockerfile -t aiminders/go:$(VERSION) .
	make push
