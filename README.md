# logagent-filter-input-grep
Apply regex to filter raw input from @sematext/logagent

# Installation 

Assuming @sematext/logagent is installed gloabally: 

```
npm i -g @sematext/logagent
npm i -g logagent-filter-input-grep
```

# Configuration 

Add following section to @sematext/logagent configuration file. Please note you could use the plugin with multiple configurations. Output of the first filter is passed into the next one ...: 

```
input: 
  files:
    - '/var/log/**/*.log'

inputFilter:
  - module: logagent-filter-input-grep
    config:
      matchSource: !!js/regexp /myapp.log/
      include: !!js/regexp /info|error/i
      exclude: !!js/regexp /test/i

output:
  elasticsearch:
    url: http://localhost:9200
    index: mylogs

```

The example above filters all log files with the content "info" or "error", and drops all lines with the keyword "test". 

Run loogagent: 
```
logagent --config myconfig.yml 
```
