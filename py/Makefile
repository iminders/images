.PHONY: cambrian py
# VERSION?=latest
# 20210111
VERSION?=1.0.0
PYTHON_VERSION?=3.8

cambrian:
	docker build -f cambrian.Dockerfile -t aiminders/cambrian:$(VERSION) .
	echo "$(DOCKER_PASSWORD)" | docker login -u $(DOCKER_USERNAME) --password-stdin
	docker push aiminders/cambrian:$(VERSION)
	docker image tag aiminders/cambrian:$(VERSION) aiminders/cambrian:latest
	docker push aiminders/cambrian:latest
	docker logout

py:
	docker build -f Dockerfile -t aiminders/python:$(PYTHON_VERSION) .
	echo "$(DOCKER_PASSWORD)" | docker login -u $(DOCKER_USERNAME) --password-stdin
	docker push aiminders/python:$(PYTHON_VERSION)
	docker image tag aiminders/python:$(PYTHON_VERSION) aiminders/python:latest
	docker push aiminders/python:latest
	docker logout