build: clean ../main.yaml

../main.yaml: main.yaml
	kustomize build >$@

main.yaml: clean/main.yaml
	kustomize build clean >$@

clean/main.yaml: clean/values.yaml
	-helm repo add bitnami https://charts.bitnami.com/bitnami
	helm repo update
	helm template jenkins bitnami/jenkins \
		--namespace=jenkins --values=clean/values.yaml --include-crds --kube-version 1.21 >$@

.PHONY: clean
clean:
	rm -f ../main.yaml main.yaml clean/main.yaml
