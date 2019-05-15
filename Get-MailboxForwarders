# Get-MailboxForwarders
# By Optoisolated
#

Function Get-MailboxForwarders
{
  param([string]$Office365AdminUser)
  $LiveCred = ""

  #Authentication 
  Get-PSSession | Remove-PSSession
  $LiveCred = Get-Credential -UserName $Username -Message "Log into Office365 instance"
  $Session = New-PSSession -ConfigurationName Microsoft.Exchange -ConnectionUri https://outlook.office365.com/powershell-liveid/ -Credential $LiveCred -Authentication Basic –AllowRedirection
  Import-PSSession $Session

  #Check Mailboxes
  $Mailboxes = Get-Mailbox
  ForEach ($Mailbox in $Mailboxes) {
      "$($Mailbox.DisplayName) - ($($Mailbox.UserPrincipalName))"
      $Rules = Get-InboxRule -Mailbox $($Mailbox.UserPrincipalName)
      $x = 0
      ForEach ($Rule in $Rules) {
          If ($Rule.ForwardTo -or $Rule.ForwardAsAttachmentTo) {
              $x++
              "  - Rule $($x): $($Rule.Name) - $($Rule.ForwardTo) - $($Rule.ForwardAsAttachmentTo)"
          }
      }
  }
}
Get-MailboxForwarders -Office365AdminUser adminuser@domain.onmicrosoft.com
