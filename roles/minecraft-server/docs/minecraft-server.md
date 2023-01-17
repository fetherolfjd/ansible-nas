# Minecraft Server

Minecraft Homepage: <https://www.minecraft.net/>

Minecraft is a popular building and exploring game.

Server Image Homepage: <https://github.com/itzg/docker-minecraft-server/>

## Usage

Set `minecraft_server_enabled: true` in your `inventories/<your_inventory>/nas.yaml` file.
If nothing else is set, a Minecraft server container with all of the default settings will
be started.

To customize the container(s) running, use the `minecraft_server_containers` variable. This
is an array of objects:

```
minecraft_server_containers:
  - cntnr_name: my_survival_server
    port: "25565"
    interactive: false
    tty: false
    addl_env: {}
  - cntnr_name: my_creative_server
    port: "25566"
    addl_env:
      MODE: creative
      SEED: "1785852800490497919"
  ...
```

Users are responsible for deconflicting container names and ports. Container names and
data directories will be prepended with `mc_srv_` so that they can be uniquely identified
by role tasks, particularly when disabled the role.

The role provides the environment values of `EULA: "TRUE"` and `ONLINE_MODE: "FALSE"` by
default for all defined containers. To change those values, simply override the variable in
the `addl_env` field of the server configuration. The role will also provide
for easy erver console access from the container via `interactive: true` and
`tty: true`. These values can be set to false to disable.