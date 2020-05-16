FROM quay.io/operator-framework/helm-operator:v0.16.0

### Required OpenShift Labels
LABEL name="Postgresql Operator" \
      vendor="OpenLabs" \
      version="v0.0.1" \
      release="1" \
      summary="This is an example of a postgresql helm operator." \
      description="This operator will deploy postgresql to the cluster."

# Required Licenses
COPY licenses /licenses

COPY watches.yaml ${HOME}/watches.yaml
COPY helm-charts/ ${HOME}/helm-charts/
