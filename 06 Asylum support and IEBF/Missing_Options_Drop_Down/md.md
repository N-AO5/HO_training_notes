
## Missing options on the drop down 
![alt text](image.png)
1. go on atlas and check that the drop down only shows a few
2. go on terminal and `source bash_profile`
3. use the cmd `eventhis [SD ID]` - The service dleivery must be of the related inbound/outbound contact (check atlas)
4. this will give a json file 
![alt text](image-1.png)
5. open finder and use cmd + shift + G and paste the path to the json file
6. open the file in vscode 
7. collapse line 2 and copy
![alt text](image-2.png)
8. cmd + a to select the whole file, cmd + v to paste the 2nd line that was just copied
9. scroll to the bottom and remove the comma
![alt text](image-3.png)
10. increase the time by one second at the bottonm
![alt text](image-4.png)
11. do the same for the top
![alt text](image-5.png)
12. copy the whole file, paste in this swagger page (click try it out)) - https://ipt-ingestion-services-prd1-prd1.service.pr.iptho.co.uk/dataplatform-services/api-doc/#/Event%20History%20V3%20APIs/DPS-EVENT-PUT-005
13. execute and the code should be 200
14. go to the psv and the menu should now have more options - resolve