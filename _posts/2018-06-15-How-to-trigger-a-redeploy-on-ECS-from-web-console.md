---
layout: post
title: "How to trigger a redeploy on ECS from web console"
author: evanbrodie
date: 2018-06-15T20:05:47+00:00
---

Sometimes, there is a neeed to trigger a redeploy on an ECS service without making any task changes (for example: rerun initialization scripts to pull secret updates). To trigger such a redeploy on an ECS service from the web console:

1. Open the ECS service module on the AWS web console
2. Click on the Cluster, then the Service you wish to trigger the redeploy on
3. Press the Update button on the top-left
4. Select the "Force new deployment" checkbox. Make no other changes. Press on the Next Step button.
5. Click "Next Step" and "Confirm" on all subsequent screens without making any other changes.

You can observe that the process is a success by watching the Events tab for new tasks startin and old tasks stopping, and the Tasks tab to witness the new tasks go live.
