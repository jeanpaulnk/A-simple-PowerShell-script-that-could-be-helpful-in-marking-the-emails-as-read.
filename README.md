Other than using exchange email clients (Outlook desktop client and outlook on the web (OWA)), you can also use PowerShell to do similar task in very efficient and automated way. Below is a simple PowerShell script that could be helpful in marking the emails as read. You can execute the script on the user's device where outlook profile is configured.
 
################
# Load the Outlook application
Add-Type -AssemblyName "Microsoft.Office.Interop.Outlook"
$Outlook = New-Object -ComObject Outlook.Application
 
# Get the MAPI namespace
$Namespace = $Outlook.GetNamespace("MAPI")
 
# Get the folder (e.g., Inbox)
$Folder = $Namespace.Folders.Item(YourEmail@domain.com).Folders.Item("Deleted Items")
 
# Iterate through all items in the folder and mark them as read
foreach ($Item in $Folder.Items) {
   if ($Item.UnRead -eq $true) {
       $Item.UnRead = $false
       $Item.Save()
   }
}
 
# Clean up
$Outlook.Quit()
[System.Runtime.Interopservices.Marshal]::ReleaseComObject($Outlook)
######################
 
Explanation:

Load the Outlook Application: This part of the script loads the Outlook application using the Microsoft.Office.Interop.Outlook assembly.

Get the MAPI Namespace: This retrieves the MAPI namespace, which is used to access the mailbox.

Get the Folder: This specifies the folder you want to modify (e.g., Deleted Items). Replace YourEmail@domain.com with your actual email address.

Iterate Through Items: This loop goes through all items in the folder and checks if they are unread. If they are, it marks them as read and saves the changes.

Clean Up: This part of the script quits the Outlook application and releases the COM object to free up resources.

Why This Method:

Efficiency: This script is efficient for handling a high volume of emails as it automates the process.

Minimal Downtime: By running this script, you can quickly change the read status of emails without manually going through each one, ensuring minimal disruption to your workflow.
