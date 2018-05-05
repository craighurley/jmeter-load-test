# Jmeter Load Testing

This is a basic jmeter project.

## Run jmeter

Populate `main.properties`, then run jmeter in headless mode:

```sh
jmeter -nt main.jmx -q main.properties -fl out/report.csv
```

Optionally, generate a report dashboard after the load test completes:

```sh
jmeter -nt main.jmx -q main.properties -fl out/report.csv -eo reports/$(date +%s)
```

For more resource intensive testing, consider tweaking the JVM arguments used by jmeter.  For example, _prepend_ the following string to the commands above (after determining an appropriate memory allocation):

```sh
JVM_ARGS="-Xms4096m -Xmx4096m -server"
```

e.g.

```sh
JVM_ARGS="-Xms4096m -Xmx4096m -server" jmeter -nt main.jmx -q main.properties -fl out/report.csv -eo reports/$(date +%s)
```

## Run jmeter (in edit mode)

Populate `main.properties`, then run jmeter in GUI mode:

```sh
jmeter -t main.jmx -q main.properties
```

## Dashboard

If you want to create a dashboard from an existing report:

```sh
jmeter -g ./out/report.csv -o reports/$(date +%s)
```

_Note: the default granularity is 60s which effects some graphs; this can be changed by editing `user.properties` (or including it in your imported properties file):_

```ini
jmeter.reportgenerator.overall_granularity=1000
```

## Links

- <https://jmeter.apache.org/>
