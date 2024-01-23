<!-- loiod5d6805daf704cd4aadd71bfdf8975d9 -->

# Git Credential Handling Using Standard Git Credential Helper

To avoid entering credentials for each Git command, configure either `git-credential-store` or `git-credential-cache`.

Before you use `git-credential-store` or `git-credential-cache`, set the `HOME` variable accordingly with the following terminal command:

```
export HOME=~
```

The tilde \(~\) corresponds to a folder named `project` that is located at the same level as the `vhome` folder.

> ### Note:  
> While the `vhome` folder is listed in the *Files* tab of the SAP Data Intelligence System Management application, the `project` folder isn't listed in the SAP Data Intelligence System Management application.



<a name="loiod5d6805daf704cd4aadd71bfdf8975d9__section_i5n_22c_rwb"/>

## git-credential-store

`git-credential-store` keeps credentials in a file in `${HOME}/.git-credentials`, which requires protection accordingly. For more information about `git-credential-store`, see the Git documentation at [https://git-scm.com/docs/git-credential-store](https://git-scm.com/docs/git-credential-store).

> ### Example:  
> `git config --global credential.helper store`



<a name="loiod5d6805daf704cd4aadd71bfdf8975d9__section_dnw_22c_rwb"/>

## git-credential-cache

`git-credential-cache` keeps the credentials in memory in a daemon process that is communicating through a socket: `${HOME}/.git-credential-cache/socket`. You can configure `git-credential-cache` timeout. For more information about `git-credential-cache`, see the Git documentation at [https://git-scm.com/docs/git-credential-cache](https://git-scm.com/docs/git-credential-cache).

`git-credential-cache` is preferred over `git-credential-store` because `git-credential-store` stores credentials on disk.

> ### Example:  
> The following Git Credential caches credentials for one day:
> 
> `git config --global credential.helper ‘cache –timeout=86400’`

`${HOME}/.git-credential-cache/` and `${HOME}/.git-credentials/` can't be located in `/vhome`.

After the container that runs the git terminal user application is recreated, re-enter the stored or cached credentials.

