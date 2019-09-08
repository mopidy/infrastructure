REPO=mopidy
IMAGE=ci-python
VERSION=`cat VERSION`

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
	docker push ${REPO}/${IMAGE}:latest
	docker push ${REPO}/${IMAGE}:${VERSION}
