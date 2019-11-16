REPO = mopidy
IMAGE = ci-python

VERSION = $(shell cat VERSION)
PYVERSION = $(shell echo ${VERSION} | cut -d - -f1)
PYMAJOR = $(shell echo ${PYVERSION} | cut -d . -f1)
PYMINOR = $(shell echo ${PYVERSION} | cut -d . -f2)
PYPATCH = $(shell echo ${PYVERSION} | cut -d . -f3)

.PHONY: build release git-release docker-release

build:
	docker build -t ${REPO}/${IMAGE}:${VERSION} .

release: git-release docker-release

git-release:
	git diff-index --quiet HEAD || (echo "Git repo is unclean"; false)
	git tag -a "${IMAGE}/${VERSION}" -m "Release ${IMAGE}:${VERSION}"
	git push --follow-tags

docker-release:
	docker tag ${REPO}/${IMAGE}:${VERSION} ${REPO}/${IMAGE}:${PYMAJOR}.${PYMINOR}
	docker tag ${REPO}/${IMAGE}:${VERSION} ${REPO}/${IMAGE}:latest
	docker push ${REPO}/${IMAGE}:${VERSION}
	docker push ${REPO}/${IMAGE}:${PYMAJOR}.${PYMINOR}
	docker push ${REPO}/${IMAGE}:latest
