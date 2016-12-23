# PowerShell: allow unsigned ps1 script to run

## Current user only
```
> Set-ExecutionPolicy -Scope CurrentUser Unrestricted
> path\to\foo.ps1
# opt.: set it back
> Set-ExecutionPolicy -Scope CurrentUser Default
```


## When in doubt, use `--force`
* run PowerShell as Administrator  
`# Set-ExecutionPolicy Unrestricted`

* user PowerShell:  
`> path\to\foo.ps1`

* (opt.) reset policy in admin shell:  
`# Set-ExecutionPolicy Restricted`