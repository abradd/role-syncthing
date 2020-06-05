# snycthing

Install syncthing and setup the folders that it is keeping synced.

## Example Inventory file.

```yaml
---
all:
  children:
    syncthing:
      host1.example.com:
      host2.example.com:
      host3.example.com:
vars:
  syncthing_folders:
    - id: asdgf-lwert
      label: Documents
      path: /home/fflintstone
  syncthing_user: fflintstone
```

## Example Playbook

```yaml
- hosts: syncthing
  become: yes
  roles:
    - syncthing
- hosts: syncthing
  become: yes
  tasks:
    - name: Sync up the folders.
      import_role:
        name: syncthing
        tasks_from: cluster
```

The first part of the playbook installs syncthing and adds a fact that pulls the syncthing machine id.

The second part causes the systems to read the new fact information and sync the folders.

## Role Variables

syncthing_user: User name.

syncthing_folders: An array containing folder information.
  * id: The unique id for the folder.
  * label: Human readable name for the folder.
  * path: The path to the folder.

syncthing_cnf_dir: Path to the syncthing configuration directory.
  * defaults to "/home/{{ syncthing_user }}/.config/syncthing"

syncthing_config: Path to the syncthing configuration file.
  * defaults to "{{ syncthing_cnf_dir }}/config.xml"

syncthing_service: Name of the syncthing service.
  * defaults to "syncthing@{{ syncthing_user }}"

## Requirements

None.

|platform|tags|
|--------|----|
|el|all (epel installation required)|
|fedora|all|

## License

MIT


