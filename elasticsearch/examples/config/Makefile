default: test
include ../../../helpers/examples.mk

RELEASE := helm-es-config

install:
	helm upgrade --wait --timeout=600 --install $(RELEASE) --values ./values.yaml ../../ ; \

secrets:
	kubectl delete secret elastic-config-credentials elastic-config-secret || true
	kubectl create secret generic elastic-config-credentials --from-literal=password=changeme --from-literal=username=elastic
	kubectl create secret generic elastic-config-secret --from-file=./watcher_encryption_key

test: secrets install goss

purge:
	helm del --purge $(RELEASE)
