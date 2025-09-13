## Mit dem Repository verbinden

### SSH-Key einrichten

-   Public Key muss in Github unter `User > Settings > SSH and GPG Keys` hinterlegt sein
-   Alias in `~/.ssh/config` erstellt

Beispiel für den Alias:

```bash
# Github Mesh Schweiz
Host github.com-meshschweiz
    HostName github.com
    User git
    IdentityFile ~/.ssh/github-meshschweiz
```

`IdentityFile` zeigt auf den Private Key.

## Repository klonen

Folgenden Befehl zum Klonen ausführen:

```
git clone git@github.com-meshschweiz:MeshSchweiz/website.git
```
