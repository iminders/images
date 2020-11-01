VERSION?=1.15

push:
	echo "$(DOCKER_PASSWORD)" | docker login -u $(DOCKER_USERNAME) --password-stdin
	docker push aiminders/go:$(VERSION)
	docker logout

build:
	docker build -f Dockerfile -t aiminders/go:$(VERSION) .
	make push

latest:
	docker build -f Dockerfile -t aiminders/go:latest .
	echo "$(DOCKER_PASSWORD)" | docker login -u $(DOCKER_USERNAME) --password-stdin
	docker push aiminders/go:latest
	docker logout
