<!-- TITLE: Embedded Power Bi Page Into Superset -->
<!-- SUBTITLE: A quick summary of Embedded Power Bi Page Into Superset -->

# Embedded PowerBI page into Superset.
1. Find the page that you want to insert the PowerBI page and insert the embedded container _div_ 
```html
<div id="embedContainer" style="width:100%; height: 800px"></div>
```
2. include __powerbi.js__ library:
```html
<script type="text/javascript" src="http://rawgit.com/Microsoft/PowerBI-JavaScript/master/dist/powerbi.js"/>
```
3. Add related javascript to render the _div_
```js
 <script type="text/javascript">
        window.onload = function f() {
            let powerbi = window.powerbi;
            // This is the  embed application access token.
            var txtAccessToken = "H4sIAAAAAAAEAB2Wxw6sihFE_-VusUSGwdJbkHPO7Mg5DBks_7vHd929quo61f_5Y6XPMKfFn3__GY_m7CK8G0ETMT8yhkycsUoDZdgaE8cAklGlYeiVKe_TNG8FUutiaknzzRCfjD0GhEqqAjJ28ECExMNax18s8bl21rdLUnrqxxEp-kQ3jfd89jDztpVDmIMEdnl6MwZV2wqPUenyL51AOMY4j_t2l3iXsJ3vDM-Wpm1HXXHiqq7rDury8QY2uHBKnBdF7mrKrVVhlTk1kMZgvBkGjeQ2x65x7l6HzRIP5Ii_r0rm8XIOznYS6-zM6kt9L_Qx5C6GSzbDYzaF_CfNZljcaH_dibKGM88fKQ_RiN5Gardoy0fLoFlQsaGhVnSQN0LYA8OSJDBVkeWT1jyB61bi3WwZO89MYvnEi53MLrjea85473e84b7dKea1crrHsuELF7maB3qpYZZcYQlt-D59Rx16SvFQbyEWFTQMAmxCa6MsXauartxihGjtgrj5KlR4Ql6kdLB6Qhp688eeOzkYzXU1BM9yLuhMkbVtz6_23IedBzTbaqaY0bzoHlRB90fEuKxDoEGv-MeBePjrI70oizNkzuFbe1nszqYyeDwUHP0oShYnzfZ3ZF6q5A_JvB4qBqwIdFa3lWsoy6QHJvROPOsLYIFgwPBuy4mqw3jZZcmG-wyy1Fi1H1PyEkpMIgWq1uoN8_3eSkCf_j4WtRbTl-RdZ2OeC2yF0krkq3I9XezBrH-ToC_dojxPGT64Ez-YrK0VToVqrpL12wMKrohFBNWZoSbe1OEP1Ln4JQiSN1zT_OyLj8TpIXo5q9eKOK5AcxV8thtUhRENte1UcQYobsCJEtbkCjvSLAt8Sw83_ZwfITXSFEW-rinjJvYpnmC5uTKT3Qat-sR9LGqBn236Pp8ru81vF8-OP9ADXzEIQfZmtG61qhsTJiqMaSeVcmOhwm143o92wDTcgY565meCpE6ci7dsZrAbD927zwjA7ltrV2HyVkMpNNVIzXZrNZHs7_CPQQHDzrF7IaJruMLfmRBcNYV794z8HjsV4Ntal6IHEHKpdtW2mnVoEIxdexfdDvZxwsl3jxUXiik6k754r7n_cKCDk4dmPdS957oNf_xiol3varNgYihg8pk0E8JeCxz15FP4ZxGCcl62PWTqW9uNBseiY3pYSZNJubfsNQIhij0aE8ka8wkxbIS6XJ-kuYh-gKmocQB96RF-NPVQXPlx6x_MFziXu2t-W1vkDLRHwjiYO1c90hxWfM-NiG6P6KYyS1lFo1FFJ16Blg1BmSsYzawZTTkMfD5COClWpA-fPYYYwmeCrKDL0zlAYii3sNSHpD9H4KGXj9I3Myh_O_dtSWvAdGY3VE_CLqjaD_8aoNHWQyNaI0ZNa2YbDr8HV0itE9ZyIQK4MYCW8lq9D-Ek0u4kTsYwwk-3qkoi5M947GfomeYot3z0QPEcX1H12T6iBi8AHYbgSJ0Wr9aTOjrQG108DBsl2mZ3JTqNjENniduL1XSlR2QP-xziwEse5lBje_Zc6mBmJPbjZKtNkuggViqWZxCYQumh_Pog2QNnElQheqZBoPLlFePQkufVotAxkAAs3UsR7Uyn0vN2ZWKYuFv12Pki0nGC1bOZsEfhXY1Kb35L_T5vF-k5oWqUlWk85XTKfixcugNZ-eEePgOT1EP5hCwqYJFjrRTlJ6T64wc8ORVZFNal0NfIznMIZRy_KmrqhNnHofONgBUyfiiCquaXnGn0fQuou3sOrL3-4GF81ZX_FFOPlRB2c3SdnmqGO0laW1v0i0XeqjEBNjfOf4cYFsOj3SE4PgtHpIHlDWC2ENU4vAa99_DwuAnF-2CNl2R-crILhx_Ny4RyYaZgFxZRW8tVWJE7NhOYfb89hk6qlC2KJ-jQomuS7LQfSeuHQFmGHV1siwidqiDN2RKK3DqR44oJyePZ7bszoAs-Cf7p6gLecu4rVx5J8igNko7KZ9SRHL_IsI3dNFdaDsElF4jXaDh-28fKx55l221R6OuUfIgkgJwveH6gtiLoE6ZHeGVqJ-tn4eZcagYeZAtiJSqkt0IQYviQWntzqPy7rI4Rmeo5_HLk_VdRXMHgETfO6rHeeRccbHp7-ztIjR9jWUeyEyfWSaw-3orlyd9gXgEd07o1i__5868_7Pos-6yWz-91KFqistZpa3AGtL_Mt_LD06vytsM7Sve2axXyjuvfiOiNzOm589WVnwTURoeR46nmw9k9J_sYDtd18Wv6oJ4EoWtCy8WSinDyDR53s8xi3SfrYsWAaohNs0wSQJLhYKxB89ChPVUWPbIzaNg1N4oItamrcKe9O1-m3ljbJ_8iT9SZqVIAavggsn7JI8C57xiS3ReGVb3R5_MR_HWY_APMuhQNoXhdo4bgSmo3xEnf6uIsrAxYebqKK0m_n5AE3qZvvHYzMSItoWdoIKxt2lWOtohiDOJ8f2Xr5Ql_sOEyaCm3TqJgW9wHTAX5bvSI8a8nrsBPdnrhVJ8i7W4ooWh5iZP1P39lfpamXOXgp_LgZBup0x_cb7rHQeETuEeR_rvltvWU7sda_tbO1S3vgsiAK0W4R4gI69tBKh4dbvfkx0gJrrTZoWCF8uDC89kfBMWWayVkJFEEndp-QthLWAY01twEM2Eo-y4yRBfHx5gJC8sYzUE1oiZSJOVv3cdfVqeE0oBhR9TJgvfh37cUYjICwvl5mcWxKQ_4qWBAhjm9XliBvFMAiVUDGUc6RHX3tOGGSIrvevVFCZoJ1ID5CVUMNgq0gsRNeRvRw-nsyjeYVr3KdM6L3E687e1VMnjcNzmLS3DmD_YyvmhBvoz-WF6zSmYbzA9PUfYwZtd8Y7q3puGbUwl67Fh3AhYs-irTYdmEO7P0sf0Ep1Z-drFK7QBGyuhS_mphVSha8X8z_vs_Z55jvi4LAAA="
            // The embed URL 
            var txtEmbedUrl = "https://app.powerbi.com/reportEmbed?reportId=8a5b15cc-e026-4d5d-94c0-db5091d65614&groupId=be8908da-da25-452e-b220-163f52476cdd";

            // Read report Id 
            var txtEmbedReportId = "8a5b15cc-e026-4d5d-94c0-db5091d65614";

            // Embed configuration used to describe the what and how to embed.
            // This object is used when calling powerbi.embed.
            // This also includes settings and options such as filters.
            // You can find more information at https://github.com/Microsoft/PowerBI-JavaScript/wiki/Embed-Configuration-Details.
            var config = {
                type: 'report',
                tokenType: 1,
                accessToken: txtAccessToken,
                embedUrl: txtEmbedUrl,
                id: txtEmbedReportId,
                permissions: 7,
                settings: {
                    filterPaneEnabled: true,
                    navContentPaneEnabled: true
                }
            };

            // Get a reference to the embedded report HTML element
            var embedContainer = $('#embedContainer')[0];

            // Embed the report and display it within the div container.
            var report = powerbi.embed(embedContainer, config);

            // Report.off removes a given event handler if it exists.
            report.off("loaded");

            // Report.on will add an event handler which prints to Log window.
            report.on("loaded", function () {
                console.logText("Loaded");
            });

            report.on("error", function (event) {
                console.log(event.detail);

                report.off("error");
            });

            report.off("saved");
            report.on("saved", function (event) {
                console.log(event.detail);
                if (event.detail.saveAs) {
                    console.log('In order to interact with the new report, create a new token and load the new report');
                }
            });
        }

    </script>
```

---
## _Reference_
Offcial sample example: 
https://microsoft.github.io/PowerBI-JavaScript/demo/v2-demo/index.html