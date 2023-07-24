# Repro repo for an issue with using hugo modules in nixos on Darwin

To reproduce, use the flake in this repo, then run `hugo mod tidy` (or anything else that would make it attempt to download a module from git).

## On macOS

```console
$ nix develop
$ hugo mod tidy
go: no module dependencies to download
go: github.com/Mitrichius/hugo-theme-anubis@upgrade: module github.com/Mitrichius/hugo-theme-anubis: git ls-remote -q origin in /tmp/nix-shell.hw4wkX/hugo_cache_asf/modules/filecache/modules/pkg/mod/cache/vcs/6af5e2ae66df69baf2c2a0f661420031722e2a6ab5e28d303d0c1ff18995ca4e: exit status 128:
    fatal: unable to access 'https://github.com/Mitrichius/hugo-theme-anubis/': OpenSSL/3.0.9: error:16000069:STORE routines::unregistered scheme
hugo: collected modules in 1257 ms
Error: failed to load modules: failed to get ["-d" "github.com/Mitrichius/hugo-theme-anubis@upgrade"]: failed to execute 'go [get -d github.com/Mitrichius/hugo-theme-anubis@upgrade]': failed to execute binary "go" with args [get -d github.com/Mitrichius/hugo-theme-anubis@upgrade]: go: github.com/Mitrichius/hugo-theme-anubis@upgrade: module github.com/Mitrichius/hugo-theme-anubis: git ls-remote -q origin in /tmp/nix-shell.hw4wkX/hugo_cache_asf/modules/filecache/modules/pkg/mod/cache/vcs/6af5e2ae66df69baf2c2a0f661420031722e2a6ab5e28d303d0c1ff18995ca4e: exit status 128:
    fatal: unable to access 'https://github.com/Mitrichius/hugo-theme-anubis/': OpenSSL/3.0.9: error:16000069:STORE routines::unregistered scheme
 *errors.errorString
 $
```

But, when getting git from /usr/bin:

```console
$ nix develop
$ env PATH=/usr/bin:$PATH hugo mod tidy
go: no module dependencies to download
go: downloading github.com/Mitrichius/hugo-theme-anubis v0.0.0-20230724084429-7ba8c815fcbe
go: added github.com/Mitrichius/hugo-theme-anubis v0.0.0-20230724084429-7ba8c815fcbe
hugo: collected modules in 1427 ms
$
```


### On NixOS/linux:
```console
$ nix develop
$ hugo mod tidy
go: no module dependencies to download
go: downloading github.com/Mitrichius/hugo-theme-anubis v0.0.0-20230724084429-7ba8c815fcbe
go: added github.com/Mitrichius/hugo-theme-anubis v0.0.0-20230724084429-7ba8c815fcbe
hugo: collected modules in 1049 ms
$
```
