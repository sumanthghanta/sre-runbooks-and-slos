# Runbook: Kubernetes Node Down

**Severity:** SEV-2
**Owner:** Platform / Infra on-call

## Alert / Symptom
- `KubeNodeNotReady` firing for one or more nodes for > 5 minutes.
- Pods stuck in `Terminating` or `Pending` due to a lost node.

## Impact
- Reduced cluster capacity; possible degraded service if pods cannot be rescheduled.
- If multiple nodes are down, customer-facing latency or errors are likely.

## Diagnosis
1. Confirm the node status:
   ```
   kubectl get nodes -o wide
   kubectl describe node <node-name>
   ```
2. Check whether the node is unreachable or genuinely down:
   ```
   ping <node-internal-ip>
   ssh <node> uptime
   ```
3. Inspect the cloud provider console for the underlying instance health.
4. Check kubelet logs if the node is reachable:
   ```
   journalctl -u kubelet --since "15 min ago"
   ```

## Mitigation
- If the node is unrecoverable, cordon and drain it so pods reschedule:
  ```
  kubectl cordon <node-name>
  kubectl drain <node-name> --ignore-daemonsets --delete-emptydir-data
  ```
- Allow the autoscaler to add a replacement node, or scale the node group manually.

## Resolution
- Verify replacement capacity is healthy and all pods are `Running`.
- Uncordon the node if it recovered, or remove it from the cluster if replaced.

## Escalation
- If capacity cannot be restored within 15 minutes, page the **Infrastructure Lead**.
- If multiple nodes fail simultaneously, declare a SEV-1 and page the incident commander.
