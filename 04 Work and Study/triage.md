
# to start
1. cmd `source bash_profile` in home direc
2. `export VAULT_ADDR=https://vault-elb.service.pr.iptho.co.uk:443 && vault login -method=ldap username=nimota.ogunwoolu` - use LDAP password
3. use `export PATH="/Users/nimota.ogunwoolu/.local/bin:$PATH"` to use the atlas toolbox 

# to end
1. git push (if changed PAT) - username `N-AO5` and password is your personal access token 

# SSB
1. to get the repo `git clone ssh://git@bitbucket.bics-collaboration.homeoffice.gov.uk/lso/lso-scripts.git`
2. cd lso-scripts
3. cd ssb_tunnel_scripts
4. `sh ssb_db_tunnel.sh`
5. test with `sh search_all.sh [UAN]` if doesnt work do step 4 again
6. use `sh resend/resend_failed_message_id.sh [error code]` to resend an error
7. DO NOT RESEND DUPLICATE ENROLMENT SSB ERRORS

# Commands 
- `uan2eventhis [UAN]` event history 
- `uan2sddetail [UAN]` get the sd id from a uan 
- `sddetails [SD]` service delivery details 
- `psv [SD]` Atlas link 
- `sh search_all.sh [UAN]` ssb (checking biometric error / error code)
- `sh resend/resend_failed_message_id.sh [error code]` error resend
- `checkSDCorrIDs [SD]` RIS check

# shortcuts
- .missingapp (missing application escalate)
- .ssberror (ssberror resolve)
- .ssbe (ssberror escalate - accenture)
- .retry (retried exception resolve)
- .resubapp (resubmit app resolve)
- .notask (no task escalate)
- .oops (oops error escalate )
- .escalate (escalate comment)
- .pp (if problems persist resolve)
- .deadline (External Enrolment Past Deadline event resolve)
- .noclearexcep (exeption that won't clear - pa atlas)
- .noexcep (no exception to clear)
- .further (further action overdue)
- .risexpired (ris expired - send to accenture)
- .risstuck (ris stuck - send to accenture)

# Tags 
- WS-IncSponsor
- WS-Registration
- WS-Merge
- **WS-Missing-App** - missing application (escalate to deloitte, .missingapp)
- **WS-OopsError** - oops error
- WS-Hops-img
- **WS-CW-R** - case worker return
- WS- MDS-Missing
- WS-NoTask
- **WS-Abort** - cw accidentally aborted an application and needs to reinstate it 
- WS-Notification-Issue
- Not-WS
- **WS-No-Issue** - no issue
- WS-SysUser
- **WS-RIS-Stuck** - incomplete ris checks (esclate to acccenture)
- WS-RIS-ExtEnr - external_enrolment-past_deadline -> resolve case
- **WS-NoRIS** - no ris checks requested 
- **WS-Bios** - resolved tickets 
- WS-RI-Person
- WS-RI-Group
- WS-DropD-Missing
- **WS-FBIS-Exception** - Fbis Fulfilment Exception
- **WS-HandffE** - handle fulfilment exceptions
- WS-HDME
- **WS-CAE** - consider application exceptions
- WS-Exception
- **C/W ...**

# Typical Event History 

1. Application is received
2. Biometric enrollment (finger print scan process, photo) (if not- do SSB check)
3. RIS checks(complete) - security checks
4. Decide / decision complete (or something similar)
5. Ready for consider/ Ready for reconsider (main thing you should see)
6. When its reconsider registration -> go back and check RIS(expire in 2month), check Sdcorrelation (command checkSDCorrIDs [service delivery ID])
7. Service delivery complete. (sometimes not showing)

# not for work and study (eg. cannot attatch photo)
1. go to slack channel #sas-tranche-1-2-3
2. "@sas_im_team [INC number] - The ticket is not for work and study, can this be reassigned?"
3. remove name from assigned on ticket 

# de-merge
1. send the INC number to the #merge-identity-queries
2. copy in your inc number
3. copy the supplier ref that they give as a reply
4. add to supplier ref box in main details of the ticket
5. send to "HODDaT - IBM Managed Identities - INC"
6. ask them to investigate the potential merge
7.  **ws-merge**

# duplicate enrolment 
1. sent to accenture 

# reopen application 
1. sd aborted in error - No option given to raise reconsideration 
2. send to PA consultant

# missing app
1. search the UAN on atlas 
2. if there - resolve no fault found
3. if not -> deloitte
4. .missingapp
5. tag **ws-missingapp**

# oops error
1. do `uan2eventhis` 
2. decison should say "TASK_COMPLETED"
3. if not 

![alt text](image-26.png)

4. copy the correlation ID 
5. search the ID in speech marks
6. change the time frame to quick -> last 30 days (but if you have the exact time and date you can search absolute)
7. add (click the little plus) message and severity on the left side 
8. there should be one green bar in the graph
9. share -> permalinks -> short URL
10. in wn .oops 
11. fill in the URL and the sddetails 
12. escalate to PA consulting atlas - .esclate
13. tag **ws-oopserror**



# Handle fulfill exceptions 
## issue -> simple error. They forgot to put city wrong, DOB correctly. Applicant error not system.

1. Put the UAN on tasklist 
2. copy the entire exception and paste in wn - REMOVE THE NAME 
3. fix the formatting 
4. get the `sddetails [SD]` fom terminal 
5. paste in wn
6. .noclearexcep
7.  assign to **PA consulting -Atlas -l3 support**
8.  tag **WS-Handffe**

# Fbis Fulfilment Exception 
1. check atlas to see of the exception is still there
2. check the UAN on tasklist 
3. retry the exception
4. if gone, double check on psv and resolve -> .retry
5. if not -> PA constulating, include sddetails -> .escalate

# no task

## no error found for app stuck 
1. check the url given by cw (copy after the /Caseworking, paste in normal atlas address in same spot)
2. check ssb -> no error
3. check ris check -> no ris stuck
4. escalate to pa consulting 

![alt text](image-27.png)

5. .escalate

## stuck on further action 
1. check `uan2eventhis [UAN]`
2. `uan2sddetail [UAN]` for further details
3. If you see " -READY_FOR_CONSIDERATION - " the application has gone through
4. use `psv [SD]` to see the consider/reconsider event history
5. check the case details - if theres a futher action delay from the customer (Comment .further)
6. the reconsider should go through after

## ssb error - no biometric enrolment
1. `uan2eventhis [UAN]`
2. appears to be stuck in ris (ris checks havent started)
3. ris checks start when biometric enrollment has been completed 
4. check psv - see if biometric enrollment has been completed  - not on atlas
5. do ssb check `sh search_all.sh [UAN]` 
6. If there is an argument in the live table - theres an error (if no error message, then there is nothing wrong)
7. run `sh resend/resend_failed_message_id.sh [error code]`
8. run `sh search_all.sh [UAN]`  again
9. if there are is no longer an error, check if the the enrolment has gone through 
10. if the error code is the same, wait and rerun cmd
11. if the error code is diffrent - send to accenture
12. run `uan2eventhis [UAN]` - there should now be a biometric enrolment
13. check psv as well - go into the grant - case details - application serice delivery details 
14. tag as **ws-bios**

## expired ris checks
1. check `uan2eventhis`
2. ris checks appear completed
3. `checkSDCorrIDs [SD]` - says all ris checks complete but might not be the case
4. `psv [SD]` check the case and see the case card - ris checks done over 2 months ago t4 expired
5. send to accenture

## ris checks haven't started
1. after checking event history, psv and ris checks
2. send to PA consultant - add sddetails

# FES STUFF w Alez Lams
- DLQ dead letter queue - Means the messages were send but not rcieved and therefore end up in the DLQ 
- SQS - simple message queues on amazon
- change the thingy to 100 messges per page
- note the queues you've done - only do ones with messages available and are DLQ

1. Log in work spaces - use nimota.ogunwoolu, LDAP, workspace MFA 
2. Go to the amazon sqs queue - https://eu-west-1.console.aws.amazon.com/sqs/v3/home?region=eu-west-1#/queues 
3. The first one - is v1 doesnt have v2 in the name 
4. V1s can only be replayed one at a time 
5. In the second DLQ Tool for v1 
6. Paste the name of the dlq you're doing - you wanna see that the number in the sqs is the same - paste in BRUNO - get list of all the letters
7. run it look at the list, copy the ACTUAL name of 

![alt text](image-32.png)

1. copy the actual name - and paste in get DLQ message

![alt text](image-30.png)

8. so the top two line and bottom two are the brackets on the next so don't count, each message is 4 lines so..
9. max number of lines - 4/ 4
10. credits expire
11. open in new tab - the first one is v1, copy the ARN into the value

![alt text](image-28.png)

1.  paste in source ARN

![alt text](image-31.png)

13. go back to the queue - go to redrive, copy the long number 

![alt text](image-33.png)

14. paste in the destination into the command 
15. paste the cmd into the terminal 

![alt text](image-34.png)


## Grey task 
 .ssbe

# SPVs and PVs
1. they have their own queue

# HOPS 

## Passport triscans missing from HOPS

![alt text](image-35.png)

![alt text](image-36.png)

![alt text](image-37.png)

1. Triscans are missing from HOPS 
2. resolve with no fault found - "Hi,

a. If the tri-scan is missing, the customer will need to be recalled and you should follow the usual process to recall the applicant

b. If the supporting evidence only is missing, but the tri scan is present, you should contact customer directly
This ticket will now be marked as resolved.

Should problems persist, please contact the ITNow Service Desk and we shall endeavour to assist.

Thanks,
SAS L2"
