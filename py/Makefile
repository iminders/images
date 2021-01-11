# VERSION?=latest
# 20210111
VERSION?=1.0.0

push:
	echo "$(DOCKER_PASSWORD)" | docker login -u $(DOCKER_USERNAME) --password-stdin
	docker push aiminders/cambrian:$(VERSION)
	docker image tag aiminders/cambrian:$(VERSION) aiminders/cambrian:latest
	docker push aiminders/cambrian:latest
	docker logout

cambrian:
	docker build -f cambrian.Dockerfile -t aiminders/cambrian:$(VERSION) .
	make push
