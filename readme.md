Repository Init Content
=======================

# Policy Quote
## Setup Project
```
cd /Users/anuragsaran/Documents/MW/summit2017/
oc project bpms-server-policyquote
oc create -f processserver-mysql-persistent-s2i.yaml
oc create -f processserver-63-is.yaml
export application_name=policyquote
export source_repo=https://github.com/anurag-saran/bxms-xpaas-policyquote-process.git
export context_dir=policyquote-process
export nexus_url=http://nexus-nexus.apps.anuragsdemo.com/
export kieserver_password=kieserver1!
export is_namespace=bpms-server-policyquote
export kie_container_deployment="policyquote-process=com.redhat.gpte.xpaas.process-server:policyquote-process:1.0-SNAPSHOT"
oc new-app --template=processserver63-mysql-persistent-s2i -p APPLICATION_NAME=$application_name,SOURCE_REPOSITORY_URL=$source_repo,CONTEXT_DIR=$context_dir,KIE_SERVER_PASSWORD=$kieserver_password,IMAGE_STREAM_NAMESPACE=$is_namespace,KIE_CONTAINER_DEPLOYMENT=$kie_container_deployment,KIE_CONTAINER_REDIRECT_ENABLED=false,MAVEN_MIRROR_URL=$nexus_url/content/groups/public/
```

## Steps for REST API
```
cd /Users/anuragsaran/Documents/MW/summit2017/bxms-advanced-infrastructure-lab/xpaas/process-server
export kieserver_password=kieserver1!
export policyquote_app=policyquote-bpms-server-policyquote.apps.anuragsdemo.com
```

## Get container ID and status


```
curl -X GET -H "Accept: application/json" --user kieserver:kieserver1! policyquote-bpms-server-policyquote.apps.anuragsdemo.com/kie-server/services/rest/server
curl -X GET -H "Accept: application/json" --user kieserver:kieserver1! policyquote-bpms-server-policyquote.apps.anuragsdemo.com/kie-server/services/rest/server/containers
```

Container ID: 19488d2672e30a5ffd510ac01ed09e29

Start a process
Update above container ID
```
curl -X POST -H "Accept: application/json" -H "Content-Type: application/json" --user kieserver:kieserver1! -d @policyquote-start-process-payload.json policyquote-bpms-server-policyquote.apps.anuragsdemo.com/kie-server/services/rest/server/containers/19488d2672e30a5ffd510ac01ed09e29/processes/policyquote.PolicyQuoteProcess/instances
```
Diff container ID.
```
curl -X POST -H "Accept: application/json" -H "Content-Type: application/json" --user kieserver:$kieserver_password -d @policyquote-start-process-payload.json "$policyquote_app/kie-server/services/rest/server/containers/policyquote-process/processes/policyquote.PolicyQuoteProcess/instances"
```
