# files-superset

Meltano project [file bundle](https://meltano.com/docs/command-line-interface.html#file-bundle) for [Superset](https://superset.apache.org/).

Files:
- [`analyze/docker-compose-non-dev.yml`](./bundle/analyze/docker-compose-non-dev.yml) 
- [`analyze/docker/*.sh`](./bundle/analyze/docker/) All the scripts used by docker-compose
- [`analyze/docker/requirments-local.txt`](./bundle/analyze/docker/requirments-local.txt) A python requirements file for extra dependencies needed.


See [setup.py](./setup.py)) for the full list of bundled files.

## Installation

To install this file bundle run the following command and provide `git+https://github.com/pnadolny13/files-superset.git` for the `pip_url`:


```bash
    meltano add files --custom superset
```

Then in order to call the docker-compose files properly you must add a custom utility to the meltano.yml manually.

```yml
  utilities:
  - name: superset
    namespace: superset
    commands:
      # meltano invoke superset:ui
      ui:
        executable: /usr/local/bin/docker
        args: compose -f analyze/superset/docker-compose-non-dev.yml up
```

If you're datasource is not included in Superset out of the box then you need to install it in the `requirements-local.txt` for it to be avaiable. See [available database drivers](https://superset.apache.org/docs/databases/installing-database-drivers) and [installation instructions](https://superset.apache.org/docs/databases/dockeradddrivers).

Lastly, invoke via `meltano invoke superset:ui`