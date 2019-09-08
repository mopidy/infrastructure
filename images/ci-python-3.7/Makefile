REPO=mopidy
IMAGE=ci-python

VERSION=`cat VERSION`
PYVERSION=`echo ${VERSION} | cut -d - -f1`
PYMAJOR=`echo ${PYVERSION} | cut -d . -f1`
PYMINOR=`echo ${PYVERSION} | cut -d . -f2`
PYPATCH=`echo ${PYVERSION} | cut -d . -f3`

.PHONY: build release

build:
	docker build -t ${REPO}/${IMAGE}:latest .

release:
	# Abort if git is unclean
	git diff-index --quiet HEAD

	# Create tags
	git tag -a "${IMAGE}/${VERSION}" -m "Release ${IMAGE}:${VERSION}"
	docker tag ${REPO}/${IMAGE}:latest ${REPO}/${IMAGE}:${VERSION}

	# Push source and image
	git push --follow-tags
	docker push ${REPO}/${IMAGE}:${VERSION}
	docker push ${REPO}/${IMAGE}:${PYMAJOR}.${PYMINOR}
	docker push ${REPO}/${IMAGE}:latest
