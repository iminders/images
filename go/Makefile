# VERSION?=latest
# 20201102
VERSION?=1.15.0

push:
	echo "$(DOCKER_PASSWORD)" | docker login -u $(DOCKER_USERNAME) --password-stdin
	docker push aiminders/go:$(VERSION)
	docker logout

build:
	docker build -f Dockerfile -t aiminders/go:$(VERSION) .
	make push
	make update_latest

update_latest:
	docker image tag aiminders/go:$(VERSION) aiminders/go:latest
	echo "$(DOCKER_PASSWORD)" | docker login -u $(DOCKER_USERNAME) --password-stdin
	docker push aiminders/go:latest
	docker logout

latest:
	docker build -f Dockerfile -t aiminders/go:latest .
	echo "$(DOCKER_PASSWORD)" | docker login -u $(DOCKER_USERNAME) --password-stdin
	docker push aiminders/go:latest
	docker logout
