# Uploading IC Test Videos

It's best to upload a video to both Prod and Opencast Dev 10.

1. Open Cisco, join vpn.dce.harvard.edu, type your HarvardKey password, handle duo
2. Open the OC Admin Dashboard: (Prod)[admin-prod.dcex.harvard.edu] or (Opencast Dev 10)[admin-dev-10.dcex.harvard.edu]
3. Click "+ Zoom"
4. Check the "Allow multiple ingests (production admin users only)"
5. Paste the "Host" recording link into "Recording Link or ID"
6. Choose the IC test series `19990189995` which should show up as: `IC Automated Test Videos (DO NOT USE FOR MANUAL TESTING)`
7. Wait for approximately second email from Opencast saying "transcripts were attached" (approx. 10min + duration of the video)
8. Open the OC Admin Dashboard
9. Click the filter icon, filter by series, paste in `19990189995`
10. Find the video, click the blue bar chart, UID = "[MPID]", Source = "ZIP-[Zoom UUID]", Location = "Zoom [MeetingId]"
11. Double click the Title, change the title, click "Save" (changes will take a few minutes to apply)

## If LHT joins/leaves:

### Update the List of Users who Have Access

1. Open Porta (Prod)[porta.dcex.harvard.edu] or (Stage)[porta-stage.dcex.harvard.edu]
2. Type "Gabe Canvas Test Students" and click "Filter"
3. Click the Person with the Pencil Icon
4. Either select and then scroll to the bottom and click "Delete"
5. OR click the person with a + and paste in HarvardKey Lite Ids

### Update Porta Permissions:

1. Open Porta (Prod)[porta.dcex.harvard.edu] or (Stage)[porta-stage.dcex.harvard.edu]
2. Paste in the series (field to the left of the "Filter" button): 19990189995
3. Select the IC Automated Test Videos course, click "Key" under "Access"
4. Select "All Resources" click the key again
5. Choose the group or search group
6. Grant access
