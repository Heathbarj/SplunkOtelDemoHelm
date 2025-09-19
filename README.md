Use a Helm Chart to deploy the CNCF OTEL demo application without the built in Otel Collector and use the included otel-demo-values.yaml to tell the Helm Chart to use the Splunk Otel Collector.


**Step 1**

Intall the Splunk Otel Collector 

Add the Splunk OpenTelemetry Collector for Kubernetes' Helm chart repository

###########

helm repo add splunk-otel-collector-chart https://signalfx.github.io/splunk-otel-collector-chart

##########


Ensure the latest state of the repository

##########

helm repo update

#########


Install the Splunk OpenTelemetry Collector for Kubernetes with the desired configuration values

##########

microk8s helm install splunk-otel-collector \
  --set "splunkObservability.accessToken=GyJQtPy8OExyIImrX0dQ1Q" \
  --set "clusterName=PI" \
  --set "splunkObservability.realm=us1" \
  --set "gateway.enabled=false" \
  --set "splunkObservability.profilingEnabled=true" \
  --set "environment=MyLabName" \
  --set "operatorcrds.install=true" \
  --set "operator.enabled=true" \
  --set "agent.discovery.enabled=true" \
  splunk-otel-collector-chart/splunk-otel-collector \
  -f https://raw.githubusercontent.com/Heathbarj/SplunkOtelDemoHelm/refs/heads/main/splunk-otel-collector-values.yaml

##########



**Step 2**

Install the OTEL Demo Application

**Step 2**
Install the OTEL Demo Application

# OpenTelemetry demo

install-otel:


helm repo add open-telemetry https://open-telemetry.github.io/opentelemetry-helm-charts 
  
  
helm repo update 


helm install otel-demo open-telemetry/opentelemetry-demo --set components.frontend-proxy.service.type=NodePort --set components.frontend-proxy.service.nodePort=30080 --set opentelemetry-collector.enabled=false -f https://raw.githubusercontent.com/Heathbarj/SplunkOtelDemoHelm/refs/heads/main/otel-demo-values.yaml

