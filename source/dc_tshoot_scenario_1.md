> \<br /\>

```{=html}
```
# Datacenter Troubleshooting Scenario 1

::: {.thumbnail align="center" width="50%"}
images/dc_tshoot_scenario_1/topo.png
:::

This troubleshooting scenario will address issues with `s1-host1` being
unable to ping `s1-host2`.

While this lab involves EVPN/VXLAN, this exercise will only require the
base knowledge of the following concepts to troubleshoot effectively, as
they are fundamental to a functioning EVPN/VXLAN environment.

1.  BGP
2.  MLAG
3.  L2 Connectivity
4.  \"Show\" commands for the concepts listed above

## Scenario Rules

1.  Datacenter2 and the border/core routers are not involved.
2.  Underlay P2P addresses have full connectivity, there are no issues
    with the interfaces themselves.
3.  There are five issues total affecting connectivity. Find all five
    problems, resolve and and test host reachibility across the fabric.

Loading The Scenario \-\-\-\-\-\-\-\-\-\-\-\-\-\--1. Provision the via
lab console and choose option (97), `Additional Labs` #. Choose option
(4), `Troubleshooting Labs` #. Choose option (3),
`Datacenter Troubleshooting Scenario 1`

Upon selecting option 3, CloudVision will automate the lab setup and
push the relevant configs to your topology.

You should see:
`Starting deployment for Troubleshooting Labs - dctshoot1 lab...`
`Gathering task information...`
`Waiting on change control to finish executing...` When complete, the
screen will exit back to the main menu and you can use option 98 to SSH
into the switches to begin the activity.
