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

Likewise, if you are developing your project using a server with limited resources, consider lowering those values, e.g:

```sh
JVM_ARGS="-Xms512m -Xmx512m -server"
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

## ulimits

When running larger tests, update the limits file (`/etc/security/limits.conf`) to include the following and then restart the server:

```ini
* soft nofile 16384
* hard nofile 16384
```

## Jmeter logging

Consider reducing the jmeter logs by editing `bin/log4j2.xml`.

### Decrease default log verbosity

Change the default log level to `warn` by changing this:

```xml
<Root level="info">
```

to this:

```xml
<Root level="warn">
```

### Increase specific loggers verbosity

Then set specific loggers to `info`, for example:

```xml
<Logger name="org.apache.jmeter.JMeter" level="info" />
<Logger name="org.apache.jmeter.threads.ThreadGroup" level="info" />
<Logger name="org.apache.jmeter.reporters.Summariser" level="info" />
```

## Links

- <https://jmeter.apache.org/>
