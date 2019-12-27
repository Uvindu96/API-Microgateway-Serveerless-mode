# API-Microgateway-Serveerless-mode

Before you begin you need to install Knative to your cluster

You can easily install Knative using following commands

1. To install Knative, first install the CRDs by running the kubectl apply command once with the -l knative.dev/crd-install=true flag. This prevents race conditions during the install, which cause intermittent errors:

kubectl apply --selector knative.dev/crd-install=true \
--filename https://github.com/knative/serving/releases/download/v0.8.0/serving.yaml \
--filename https://github.com/knative/eventing/releases/download/v0.8.0/release.yaml \
--filename https://github.com/knative/serving/releases/download/v0.8.0/monitoring.yaml

2. To complete the install of Knative and its dependencies, run the kubectl apply command again

kubectl apply --filename https://github.com/knative/serving/releases/download/v0.8.0/serving.yaml \
--filename https://github.com/knative/eventing/releases/download/v0.8.0/release.yaml \
--filename https://github.com/knative/serving/releases/download/v0.8.0/monitoring.yaml

3. Monitor the Knative components until all of the components

kubectl get pods --namespace knative-serving
kubectl get pods --namespace knative-eventing
kubectl get pods --namespace knative-monitoring

All the trafic for the Knative service is handled by Istio, you need to enbale Istio-injection for enble trafic routing using istio

    kubectl label namespace default istio-injection=enabled

Now you are all set to deploy your Knative service...

    kubectl apply -f knative_service.yaml

To check the pod status for your deployment, you can use following command

    kubectl get pods
