# Throttle plugin
It discards the events if pipeline throughput gets higher than a configured threshold.

### Config params
**`throttle_field`** *`cfg.FieldSelector`* 

The event field which will be used as a key for throttling.
It means that throttling will work separately for events with different keys.
If not set, it's assumed that all events have the same key.

<br>

**`time_field`** *`cfg.FieldSelector`* *`default=time`* 

The event field which defines the time when event was fired.
It is used to detect the event throughput in a particular time range.
If not set, the current time will be taken.

<br>

**`time_field_format`** *`string`* *`default=rfc3339nano`* *`options=ansic|unixdate|rubydate|rfc822|rfc822z|rfc850|rfc1123|rfc1123z|rfc3339|rfc3339nano|kitchen|stamp|stampmilli|stampmicro|stampnano`* 

It defines how to parse the time field format.

<br>

**`default_limit`** *`int64`* *`default=5000`* 

The default events limit that plugin allows per `interval`

<br>

**`buckets_count`** *`int`* *`default=60`* 

How much time buckets to hold in the memory. E.g. if `buckets_count` is `60` and `interval` is `5m`,
then `5 hours` will be covered. Events with time later than `now() - 5h` will be dropped even if threshold isn't exceeded.

<br>

**`bucket_interval`** *`cfg.Duration`* *`default=1m`* 

Time interval to check event throughput.

<br>

**`rules`** *`[]RuleConfig`* 

Rules to override the `default_limit` for different group of event. It's a list of objects.
Each object has the `limit` and `conditions` fields.
* `limit` – the value which will override the `default_limit`, if `conditions` are met.
* `conditions` – the map of `event field name => event field value`. The conditions are checked using `AND` operator.

<br>


<br>*Generated using [__insane-doc__](https://github.com/vitkovskii/insane-doc)*