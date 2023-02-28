# MicrosoftActionsByDefaultRoles

Two different CSVs that contain the default roles and actions enabled by Microsoft. Meant to make it easier to find roles with specific capabiliites.

# Diff

- Roles.Csv just has two columns | ROLE | ACTION |
- Roles_Split.csv attempts to logically breakdown the actions into columns

# Do it yourself!
```
## Powershell 5/7
Import-Module -Name Microsoft.Graph

Connect-MgGraph # Connects to Microsoft Graph
$RoleDefinitions = Get-MgRoleManagementDirectoryRoleDefinition

# Create the roles file
"Role,Action" > "Roles.csv"

# Get the actions per role
ForEach($RoleDef in $RoleDefinitions) {
    ForEach($Action in $RoleDef.RolePermissions.AllowedResourceActions) {
        "$($RoleDef.DisplayName),$($Action)" >> Roles.csv
    }
}
```