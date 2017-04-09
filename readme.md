Repository Init Content
=======================

Your project description here.


cd /Users/anuragsaran/Documents/MW/summit2017/bxms-advanced-infrastructure-lab/xpaas/process-server
export kieserver_password=kieserver1!
export policyquote_app=policyquote-bpms-server-policyquote.apps.anuragsdemo.com

curl -X GET -H "Accept: application/json" --user kieserver:kieserver1! policyquote-bpms-server-policyquote.apps.anuragsdemo.com/kie-server/services/rest/server
curl -X GET -H "Accept: application/json" --user kieserver:kieserver1! policyquote-bpms-server-policyquote.apps.anuragsdemo.com/kie-server/services/rest/server/containers
Container ID: 19488d2672e30a5ffd510ac01ed09e29

Start a process
curl -X POST -H "Accept: application/json" -H "Content-Type: application/json" --user kieserver:kieserver1! -d @policyquote-start-process-payload.json policyquote-bpms-server-policyquote.apps.anuragsdemo.com/kie-server/services/rest/server/containers/19488d2672e30a5ffd510ac01ed09e29/processes/policyquote.PolicyQuoteProcess/instances

curl -X POST -H "Accept: application/json" -H "Content-Type: application/json" --user kieserver:$kieserver_password -d @policyquote-start-process-payload.json "$policyquote_app/kie-server/services/rest/server/containers/policyquote-process/processes/policyquote.PolicyQuoteProcess/instances"
