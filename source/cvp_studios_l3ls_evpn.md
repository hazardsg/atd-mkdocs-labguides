> \<br /\>

```{=html}
```
# CloudVision Studios - L3LS/EVPN LAB GUIDE

::: {.thumbnail align="center"}
images/cvp_studios_l3ls_evpn/1TOPO.PNG
:::

| 

-   The \"Datacenter1\" topology for this lab consists of two
    **spines,** four **leafs**, and two **\"hosts\"** for reachability
    testing.
-   The borderleafs, cores, and Datacenter 2 are not a part of this lab
    guide.
-   The hosts will be pre-configured as L2 LACP trunk port-channels up
    to their respective leafs.
-   VLAN 60 and 70 will be pre-configured with SVIs on each host for
    post change reachability testing.

\* All underlay addressing will be performed by CVPS. The hosts are
already configured via lab configlets, we will not be involving them in
the Studios process.

First, on the lab topology landing page, click on **Console Access** and
provision the lab by running option 6,
`CVP lab for Studios L3LS/EVPN (studiosl3ls)` Allow the task to
complete, and proceed to step 1.

::: {.thumbnail align="center"}
images/cvp_studios_l3ls_evpn/0jumpbox.png
:::

| 

Click on **CVP** on the topology landing page to access CloudVision
Portal

1.  Workspace Creation

    a.  Navigate to **Provisioning** on the top menu, then click on
        **Studios** on the left, then click the **Create Workspace**
        button. Name it **\"LAB\"** then click **Create**

    b.  Once created, click on **\"Inventory and Topology\"** to enter
        the Inventory \"studio\"

        ::: {.thumbnail align="center"}
        images/cvp_studios_l3ls_evpn/2WorkspaceIntro.gif
        :::

    :::: note
    ::: title
    Note
    :::

    The term \"studio\" is used to describe the pre-built configuration
    sections within CloudVision Studios. These include Connectivity
    Monitoring, Date and Time, Interface Configuration, Postcard
    Telemetry, Streaming Telemetry Agent, Campus Fabric, Enterprise
    Routing, L3 Leaf-Spine Fabric, EVPN Services, and Segment Security.
    ::::

2.  Inventory studio

    a.  You are now looking at the Inventory studio, where we will
        select the devices we would like to configure.
    b.  We will start adding devices into our workspace by clicking the
        **Accept Updates** tab.
    c.  Select both site 1 spines: `S1-Spine1 and S1-Spine2` as well as
        the leafs in site1: `S1-Leaf1, S1-Leaf2, S1-Leaf3, S1-Leaf4`,
        Ignore anything else.
    d.  Click **\"Accept Updates\"**.
    e.  Notice that there are devices now in the **\*onboarded devices**
        section.
    f.  Enter the device and see how Studios has detected the topology
        connections.

    ::: {.thumbnail align="center"}
    images/cvp_studios_l3ls_evpn/3Inventory.gif
    :::

    :::: note
    ::: title
    Note
    :::

    This is where we will tell studios which devices to include, and the
    studio will know how the physical topology is built via lldp. It
    will allow the other studios to auto detect links to assign properly
    for a functional network.
    ::::

1.  Workspace Review

    :::: note
    ::: title
    Note
    :::

    We created our workspace named \'LAB\' at the beginning of this lab.
    You can make a separate workspace for every studio if you wish,
    however for this lab we are going to do all this work in the same
    workspace, because we would like to demonstrate how this process
    builds on itself in the staging area.
    ::::

    Click on **Review Workspace** on the upper right. This will take us
    to the **Workspace Summary** page to store the inputs for this
    studio to the staging area for later use. Once we click review, it
    will run through the checks and tell us if we are good to proceed.
    You can see in the workspace summary what studios have been
    modified.

    ::: {.thumbnail align="center"}
    images/cvp_studios_l3ls_evpn/4InventoryBuild.PNG
    :::

    | 

2.  L3LS Studio

    The L3LS studio is a powerful and flexible tool to get our underlay
    topology up and running quickly. In this lab we will have the studio
    \"autotag\" our devices to assign them. There are user tags and tags
    the system creates using the *\"auto tagger\"* as the studio is
    configured. Tags are formed in a **label:value format.** E.G. `DC:1`
    In studios there are three assignment methods. **All Devices**,
    **Device By Tag Query**, and **No Devices**. For the purposes of
    this lab and to demonstrate the tag system we will be using **Device
    By Tag Query**

    ::: {.thumbnail align="center"}
    images/cvp_studios_l3ls_evpn/5tagexample.png
    :::

    a.  Navigate to the **Provisioning\>Studios\>L3 Leaf-Spine Fabric**
        studio.
    b.  Under *Data Centers*, click **Add Data Center** to add a DC,
        name it **1**, and click **+ Create \"1\"**. This will establish
        a tag pair of `DC:1`
    c.  Click **Edit** next to Device Selection, then click the drop
        down menu and choose **Tag Query**
    d.  Use the tag pair of `DC:1` (You may ignore the message that says
        No Devices Found\" since we haven\'t assigned this tag to any
        devices yet)
    e.  Once complete, click the arrow next to DC 1 in the Datacenter
        section to proceed into the configuration.

    *(The DC name can be a name or an integer, but for the lab use the
    aforementioned value)*

    ::: thumbnail
    images/cvp_studios_l3ls_evpn/6l3ls.gif
    :::

    f.  Assign devices to the DC by clicking on the **Assigned Devices**
        field and clicking each individual device.
    g.  Under the Role section below, specify `Leaf` or `Spine` where
        needed.
    h.  Create Pod, name as **1** and ignore the warning on creation.
    i.  Enter Pod configuration by clicking the arrow.

    ::: {.thumbnail align="center"}
    images/cvp_studios_l3ls_evpn/7l3ls.gif
    :::

    j.  Assign all devices to the Pod via \"Assigned Devices\"
    k.  Add the two spines to the Spines section. number `s1-spine1` as
        1, `s1-spine2` as 2.
    l.  Add L3 Leaf Domain 1 and 2
    m.  In Leaf Domain 1 add `s1-leaf1`, number as 1, `s1-leaf2`, number
        as 2.
    n.  In Leaf Domain 2 add `s1-leaf3`, number as 3, `s1-leaf4`, number
        as 4.

    ::: {.thumbnail align="center"}
    images/cvp_studios_l3ls_evpn/8l3ls.gif
    :::

    :::: warning
    ::: title
    Warning
    :::

    Leaf Domains *MUST* be an integer or the build process will fail.
    Also, in a Pod all switches in a role **MUST** have a unique number
    or the build process will fail.
    ::::

    :::: note
    ::: title
    Note
    :::

    A leaf domain can be a pair of switches or a standalone. MLAG
    configuration is the default when domains are a pair.
    ::::

    The next step is to review the **workspace**. But before we do that,
    have a good look at the lower section. These are all the variables
    that the topology will be built on. For this lab we'll leave it all
    at defaults. Noteworthy are those blue knobs below. Some options are
    BGP dynamic listeners on the Spines, VXLAN Overlay, topology
    settings for EVPN, etc. If all you wanted was strictly L3LS as a
    foundation you could turn off VXLAN/EVPN if you so chose.

    ::: {.thumbnail align="center"}
    images/cvp_studios_l3ls_evpn/9l3ls.gif
    :::

    This studio is complete, click **Review Workspace** in the upper
    right. CloudVision will now take all the inputs made to the studio
    and build the switch configurations. At the end of the build there
    should be three green checkmarks. Once the build is complete, do
    **NOT** click on **Submit Workspace.** Note the Workspace Summary
    shows the studios modified, and tag changes. Let\'s go the the tag
    section for a moment.

    o.  Click on the **Tags** section in the Provisoning menu.
    p.  Click on `s1-leaf1` and observe the tags the studio assigned.
    q.  Do the same with `s1-spine1`

    ::: {.thumbnail align="center"}
    images/cvp_studios_l3ls_evpn/10tags.png
    :::

    The tags are what allows studios to determine the logical and
    physical relationships of the switches in the fabric. Let\'s move
    onto the next section, EVPN.

3.  EVPN Studio

    Part of what makes Studios so powerful is the ability to pull
    information/inputs from other studios. The EVPN studio is very
    flexible and quick to configure, as it will pull all underlay
    inforamtion form L3LS. You will see these examples are we proceed.
    As EVPN focuses on the leafs, we will only be concerned with the
    leafs. To show the flexibility of the query engine, our search query
    for assignment will be `DC:1 AND Role:Leaf`

    a.  Navigate to the **Provisioning\>Studios\>EVPN Services** studio.
    b.  Use `DC:1 AND Role:Leaf` as the query
    c.  Create the tenant, called **"A"**
    d.  Enter the tenant configuration
    e.  Create a VRF, called \"**A**\"
    f.  Enter the VRF configuration
    g.  Set the VNI to `50000`
    h.  Exit back to tenant to configure vlans.

    :::: note
    ::: title
    Note
    :::

    The only **required** entry in the VRF is the **VNI** The **VNI**
    can be any value, provided it does not conflict with the base VNI
    VLANS will get auto assigned with (though you can override the VNI
    on the VLAN page) For lab purposes we will set the **VNI** as
    `50000`
    ::::

    ::: {.thumbnail align="center"}
    images/cvp_studios_l3ls_evpn/11evpn.gif
    :::

    Next, VLANs 60 and 70 will be configured in the tenant.

    j.  Create VLAN ID 60
    k.  Enter the configuration for VLAN 60
    l.  Add VTEP, using `DC:1 AND Role:Leaf` as the query
    m.  Enter the VTEP configuration to allow the tags to be assigned
        automatically
    n.  Exit the VTEP configuration
    o.  Under VRF, choose **A**
    p.  Set the SVI Virtual IP Address to `10.60.60.1/24`
    q.  Exit back to the tenant, and create VLAN 70 with the same
        process.
    r.  Set the VLAN 70 SVI Virtual IP Address to `10.70.70.1/24`

    Notice when entering the VTEP config the router_bgp.router_id and
    router_bgp.as variables are auto-filled. The studio is pulling this
    information directly from the information stored from the L3LS
    studio we finished earlier in this lab.

    ::: {.thumbnail align="center"}
    images/cvp_studios_l3ls_evpn/12evpn.gif
    :::

    :::: warning
    ::: title
    Warning
    :::

    You MUST enter the VTEP configuration area for each VLAN in order
    for the tags to automatically assign. Failure to complete this step
    will cause the VTEP configuration to not be saved for the build
    process .
    ::::

    As the final configuration step of this studio, create the vlan
    aware bundle. VLAN Bundles are optional, and If you are cross
    vendor, you might not be able to use them.

    s.  In the Tenant, click on **Add Vlan Aware Bundle** and name it
        **\"Bundle\"**
    t.  Enter the configuration, set the vlan range to `60,70`
    u.  Exit back to the tenant

    We're done with the EVPN studio. Click **Review Workspace** and then
    start the build.

    ::: {.thumbnail align="center"}
    images/cvp_studios_l3ls_evpn/14evpn.gif
    :::

    The last Studio before submitting the workspace to Change Control
    will be the Interface Studio for the leaf to host connectivity.

4.  Interface Studio

    Let's take another look at the topology. The leafs are connected to
    the hosts on `E4` and `E5`. The hosts are already pre configured for
    PO1 on ports `E1-2` in LACP. The hosts are also configured via
    **console option 6** in vlan 60 and 70 with respective SVIs for
    testing. Let's navigate to the Interface Studio and start the
    configuration.

    ::: {.thumbnail align="center"}
    images/cvp_studios_l3ls_evpn/16interface.png
    :::

    a.  Navigate to the **\'Provisioning\>Studios\>Interface
        Configuration"** studio.
    b.  Leave the query as \"All Devices\"
    c.  Create a profile, named **"MLAG-PO"**, and enter configuration.
    d.  Set as **trunk port**, set native VLAN of **"1"**, allow
        `vlan60` and `vlan70`, set PO to **\"1\"**, check **"yes"** for
        mlag.
    e.  Apply the profile to port `E4` on each leaf.

    ::: {.thumbnail align="center"}
    images/cvp_studios_l3ls_evpn/17interface.gif
    :::

    :::: warning
    ::: title
    Warning
    :::

    The **MLAG** and **LACP** options are hidden until a PO number is
    entered. Ensure you scroll after completing the PO to ensure both
    are set to Yes.
    ::::

    Click On **Review Workspace** and allow for the build to complete.

    ::: {.thumbnail align="center"}
    images/cvp_studios_l3ls_evpn/18interface.gif
    :::

5.  Final Revew and Submission to Change Control

    :::: note
    ::: title
    Note
    :::

    We are going to commit this workspace as a final build to the
    network fabric. Once we submit, this workspace will close out and it
    cannot be modified. However, the inputs are then committed to
    Studios (the repository) This allows new workspaces to use those
    same inputs to perform Day2 change/add/remove actions.
    ::::

    a.  After the build completes, you should see a \"Build Succeeded\"
        message at the top.
    b.  Click **"Submit Workspace"** to close the workspace and create
        the Change Control.
    c.  Click **"View Change Control"** to be taken to Change Control.
    d.  **"Review and Approve"** to prep the changes to the network.
    e.  Run the changes in parallel, and choose **\"execute
        immediately\"** to apply to devices.
    f.  Click **"Approve and Execute"**.

    :::: note
    ::: title
    Note
    :::

    The gif of the change control process has been compressed for time.
    Actual change control time was about 1 minute.
    ::::

    ::: {.thumbnail align="center"}
    images/cvp_studios_l3ls_evpn/19CC.gif
    :::

    All tasks should complete successfully, and we can move onto the
    verification part of the lab.

6.  Lab Verification

    a.  Log into the Spines and run **sh bgp summary**
    b.  Verify underlay and overlay BGP adjacencies are **Established**.
    c.  Repeat for Leafs. Outputs should be similar.

    SPINES - BGP Summary

    ``` bash
    Neighbor               AS Session State AFI/SAFI                AFI/SAFI State   NLRI Rcd   NLRI Acc
    172.16.0.3          65001 Established   L2VPN EVPN              Negotiated              4          4
    172.16.0.4          65001 Established   L2VPN EVPN              Negotiated              4          4
    172.16.0.5          65002 Established   L2VPN EVPN              Negotiated              4          4
    172.16.0.5          65002 Established   L2VPN EVPN              Negotiated              4          4
    172.16.0.6          65002 Established   L2VPN EVPN              Negotiated              4          4
    172.16.200.1        65001 Established   IPv4 Unicast            Negotiated              7          7
    172.16.200.5        65001 Established   IPv4 Unicast            Negotiated              7          7
    172.16.200.9        65002 Established   IPv4 Unicast            Negotiated              7          7
    172.16.200.13       65002 Established   IPv4 Unicast            Negotiated              7          7
    ```

    LEAFS - BGP Summary

    ``` bash
    Neighbor               AS Session State AFI/SAFI                AFI/SAFI State   NLRI Rcd   NLRI Acc
    172.16.0.1            65000 Established   L2VPN EVPN              Negotiated              8          8
    172.16.0.2            65000 Established   L2VPN EVPN              Negotiated              8          8
    172.16.200.0          65000 Established   IPv4 Unicast            Negotiated             10         10
    172.16.200.2          65000 Established   IPv4 Unicast            Negotiated             10         10
    192.168.255.255       65001 Established   IPv4 Unicast            Negotiated             13         13
    ```

    d.  Verify MLAG on the Leafs. On Leafs 1-4 run the **"show mlag"**
        command

    e.  Verify all Leafs show as **"Active"** and **"Up-Up."**

        ``` bash
        MLAG Status:                     
        state                              :              Active
        negotiation status                 :           Connected
        peer-link status                   :                  Up
        local-int status                   :                  Up
        ```

    f.  On leaf 1 and 3 verify the Port-Channel status.

    g.  Run the command **"sh port-channel dense"**

    ``` bash
    Port-Channel       Protocol    Ports             
    Po1(U)            LACP(a)     Et1(PG+) Et2(PG+) PEt1(P) PEt2(P)
    ```

    :::: note
    ::: title
    Note
    :::

    MLAG has an enhancement with the port-channel command. It show the
    status of the port channel across both switches. The output shows
    this status of the MLAG PortChannel. See the local switch as well as
    the peer, with the **(P)** being the opposite switch.
    ::::

    Now that we've confirmed all the base connectivity, let's test the fabric and look at some outputs.

    :   h.  Ping the gateway at **10.60.60.1**. from `s1-host1`.
        i.  Ping the SVI local to the switch at at **10.60.60.160**.
            from `s1-host1`.
        j.  Ping across the fabric in the same vlan, from `s1-host1`
            **10.60.60.160** to `s1-host2` **10.60.60.161.**
        k.  Ping across the fabric intervlan from `s1-host1`
            **10.60.60.160** to `s1-host2` **10.70.70.171.**
        l.  On `s1-leaf1`, review the EVPN routing table using **"show
            bgp evpn"**.
        m.  On `s1-host1` and on `s1-host2` do **"show int vlan 60"**
            and make note of their **mac.**
        n.  On `s1-leaf1`, do `“show mac address-table vlan 60”`.
        o.  notice `s1-host1’s` mac comes across PO1 and `s1-host2’s`
            comes across Vx1.

**LAB COMPLETE!**
