# Policies order/wave

In this document we try to summarize when the different main waves, and which configurations are done there.

The following command, used on the hub (or spoke), can show you all the policies and the waves when these happen. 

```yaml
oc -n <CLUSTER_NAME> get policies -o json | jq -r '.items[] | "Policy: " + .metadata.name + "  on wave: " + .metadata.annotations."ran.openshift.io/ztp-deploy-wave"' | sort -g -t ":" -k 3
```

In general we will try to follow these main waves:

wave 1: whatever (if needed) before pausing the MCP

wave 5: Paused MCPs

wave 6: some generic configurations and network

wave 8: in this moment all the operators are installed

wave 10: all the configurations related to operators

wave 15: UnPaused MCPs, above this wave, Policies should not do anything that will make cluster reboot

wave 10000: at the very end, the validation of the cluster
