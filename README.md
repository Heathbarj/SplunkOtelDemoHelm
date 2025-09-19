Use a Helm Chart to deploy the CNCF OTEL demo application without the built in Otel Collector and use the included otel-demo-values.yaml to tell the Helm Chart to use the Splunk Otel Collector.

# -----------------------------------------------------------------------
**Step 1**

Intall the Splunk Otel Collector 
# -----------------------------------------------------------------------
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
helm install splunk-otel-collector --set="splunkObservability.accessToken=<YOURACCESSTOKEN>,clusterName=<YOURCLUSTERNAME>.splunkObservability.realm=<YOURREALM>,gateway.enabled=false,splunkObservability.profilingEnabled=true,environment=unknown,operatorcrds.install=true,operator.enabled=true,agent.discovery.enabled=true" splunk-otel-collector-chart/splunk-otel-collector -f https://github.com/Heathbarj/SplunkOtelDemoHelm/blob/main/otel-demo-values.yaml
##########



**Step 2**

Install the OTEL Demo Application
# -----------------------------------------------------------------------
**Step 2**
Install the OTEL Demo Application
# OpenTelemetry demo
# -----------------------------------------------------------------------
install-otel:


HELM repo add open-telemetry https://open-telemetry.github.io/opentelemetry-helm-charts 
  
  
HELM repo update 


HELM  --install otel-demo open-telemetry/opentelemetry-demo --set components.frontend-proxy.service.type=NodePort --set components.frontend-proxy.service.nodePort=$(OTEL_PORT) --set opentelemetry-collector.enabled=false -f https://github.com/Heathbarj/SplunkOtelDemoHelm/blob/main/splunk-otel-collector-values.yaml
