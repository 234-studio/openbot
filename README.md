# openbot

Repo do wdrożenia [OpenBot](https://openbot.run) jako usługi **Compose** w Easypanelu.

Obraz: `ghcr.io/nightly-labs/openbot:0.59.0` (tag z [nightly-labs/openbot@v0.59.0](https://github.com/nightly-labs/openbot/tree/v0.59.0)).  
`seccomp.json` skopiowany 1:1 z tego taga.

## Logowanie

Logowanie w konsoli kontenera:

```bash
openbot login --name ...
```

Kod z maila nie trafia do wiadomości ani do tego repo. Sekrety nie są tu przechowywane.

## Bezpieczeństwo

- **Nie montuj:** `docker.sock`, `/etc/easypanel`, katalogów domowych hosta, sekretów z hosta.
- **Nie używaj:** `privileged`, `network_mode: host`, `seccomp=unconfined`, publikowanych portów.
- Wolumen tylko `openbot-data` → `/data`.
- `shm_size: 1g`, `no-new-privileges`, własny `seccomp.json`.

## Upgrade

1. Backup wolumenu `/data` (stan konta i dane).
2. Zmień tag obrazu w `docker-compose.yml` (np. `0.59.0` → nowszy).
3. Deploy w Easypanelu.
4. OpenBot nie wraca do starszej wersji — nie obniżaj taga.

## Źródła

- Oficjalny compose: `docker/compose.yaml` w tagu `v0.59.0`
- Oficjalny seccomp: `docker/seccomp.json` w tagu `v0.59.0`
- Dokumentacja: https://github.com/nightly-labs/openbot/blob/v0.59.0/docs/docker.md
