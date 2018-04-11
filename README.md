# Logstash

Setup a logstash instance.


## Requirements

An apt based linux system

## Role Variables

| Variable                | Default / Mandatory                                             | Description                                                                                                                                                                                                                                              |
|-------------------------|-----------------------------------------------------------------|----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| `logstash_config`       | `{ path: { logs: /var/log/logstash, data: /var/lib/logstash }}` | Since the logstash settings file is a yaml file we write the whole object to the settings file. For more Information please see the [logstash settings file documentation](https://www.elastic.co/guide/en/logstash/current/logstash-settings-file.html) |
| `logstash_config_files` | `{}`                                                            | Dictionary of config files to write to conf.d/. More information below.                                                                                                                                                                                  |

### `logstash_config_files`
Each entry in the `logstash_config_files` consists out of the following entries.
The key of each entry has to be unique and will be used for the config file name.

| Variable | Default / Mandatory | Description                                           |
|----------|---------------------|-------------------------------------------------------|
| `input`  | :heavy_check_mark:  | Input definition of the config file.                  |
| `filter` | `null`              | Filter definition of the config file.                 |
| `output` | :heavy_check_mark:  | Output definition of the config file.                 |

## Example Playbook

```yml
- hosts: all
  become: true
  vars:
    logstash_config_files:
      - name: syslog
        input: |
          file {
            path => "/var/log/nginx/*.log"
            }
        output: |
          elasticsearch {
            hosts => ["elasticsearch.example.de"]
          }
```

## License

This work is licensed under a [Creative Commons Attribution-ShareAlike 4.0 International License](https://creativecommons.org/licenses/by-sa/4.0/).

## Author Information

- [Fritz Otlinghaus (Scriptkiddi)](https://github.com/scriptkiddi) _fritz.otlinghaus@stuvus.uni-stuttgart.de_
