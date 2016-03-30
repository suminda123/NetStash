# NetStash
Logstash sender for .NET

Send events to logstash instance via TCP

Saves all events into a sqlite database to prevent loss from network issues

Automatic synchronization when network connection is stablished

## Usage

```
NetStashLog log = new NetStashLog("brspomelkq01.la.imtn.com", 1233, "NSTest", "NSTestLog");

Dictionary<string, string> vals = new Dictionary<string, string>();
//Additional fields
vals.Add("customerid", "1235");

log.Error("Testing", vals);
```

## Logstash config

```
input {
  tcp {
    port => 1233
    host => "10.32.12.52"
    codec => json
  }
}
filter {
  mutate { gsub => ["message", "@($NL$)@", "\r\n"] }
}
output {
  elasticsearch {

  }
}

```

## Who is using

Iron Mountain Brasil
 - All internals logs systems.