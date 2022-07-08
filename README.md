# workflow-status
Custom dashboard for workflow run details


Status Badge

- Push

[![demo_workflow](https://github.com/vpulagarwal/workflow-status/actions/workflows/sample.yml/badge.svg?branch=main&event=push)](https://github.com/vpulagarwal/workflow-status/actions/workflows/sample.yml)

- Workflow Dispatch


[![demo_workflow](https://github.com/vpulagarwal/workflow-status/actions/workflows/sample.yml/badge.svg?branch=main&event=workflow_dispatch)](https://github.com/vpulagarwal/workflow-status/actions/workflows/sample.yml)


- Other params:


| Workflow  | Event Type | Actor | Inputs | Last run date and time | Last Run Status |
| ------------- |:-------------:|:-------------:|:-------------:|:-------------:|:-------------:|
| left foo      | right foo     |
| left bar      | right bar     |
| left baz      | right baz     |



Timezone db: https://en.wikipedia.org/wiki/List_of_tz_database_time_zones




- name: Set current date as env variable
  run: echo "WORKFLOW_DATE_TIME=$(TZ=":Asia/Calcutta" date +'%Y-%m-%dT%H:%M:%S')" >> $GITHUB_ENV
- name: Echo WORKFLOW_DATE_TIME
  run: echo "${{ env.WORKFLOW_DATE_TIME }}"
- name: echo actor
  run: echo ${{ github.actor }}
- name: echo event name
  run: echo ${{ github.event_name	}}
- name: echo file at event path
  run: cat ${{ github.event_path }}
- name: check jq
  run: jq .inputs ${{ github.event_path }}
- name: Create JSON Object
  run: | 
    jq -n \
    --arg workflow "${{ github.workflow }}" \
    --arg actor "${{ github.actor }}" \
    --arg event_name "${{ github.event_name }}" \
    --arg WORKFLOW_DATE_TIME "${{ env.WORKFLOW_DATE_TIME }}" \
    --argjson inputs "$(jq .inputs ${{ github.event_path }})" \
    '$ARGS.named'