# Hugo deployment

The October 27 operations record still describes a WordPress blog. The November 3 host review records Hugo and the systemd blog deployment timer and service on Server1. This page covers the newer Hugo workflow.

**GitHub revision → systemd timer and service → Hugo build check → publish → check the public site**

| Stage | Operator procedure |
| --- | --- |
| Pull | Let the timer trigger the deployment service and identify the Git revision being built. A timer invocation is evidence of a trigger. Review the service result to establish whether the run succeeded. |
| Build and validate | Build Hugo output and check the build exit status and expected pages before promoting the output. On a failed build, stop publication and investigate the build result. |
| Publish and verify | Serve the validated output through Caddy. Check the public entry page and a representative article through Cloudflare, including expected assets and HTTPS behavior. |
| Roll back | If publication causes a regression, rebuild and republish the last known-good Git revision, then repeat the public checks. Revert the offending change in GitHub before normal scheduled deployment resumes so the timer does not pick it up again. |

The host review confirms the timer and pull/build workflow. The validation and rollback steps describe the operating procedure. The available records do not establish an executed rollback drill, an atomic publish mechanism, or automatic rollback.

[Back to overview](../README.md)
