###
# ElastAlert
###
installation
```
https://elastalert.readthedocs.io/en/latest/running_elastalert.html#tutorial

1. python3 -V #should be 3.6
2. sudo apt install python-pip python-dev libffi-dev libssl-dev

1. sudo apt install python3-pip
2. pip3 install elastalert
3. pip install "elasticsearch>=7.11.0"
4. git clone https://github.com/Yelp/elastalert.git
5. sudo python3 setup.py install
```
#ElastAlert set-up

```
1. cp config.yaml.example config.yaml
2. sudo nano /elastalert/config.yaml

In the config file:

3. es_host: 10.0.2.15
4.  es_username: elastic     
    es_password: 3last1c 
```
# Stack Management/Index patterns

```
sudo apt install elastalert

1. elastalert-create-index
```
elasticsearch.exceptions.RequestError: RequestError(400, u'illegal_argument_exception', u'Types cannot be provided in put mapping requests, unless the include_type_name parameter is set to true.')
sk1f@vb:/elastalert/example_rules$ es.indices.put_mapping(index='my_index', body=my_mapping, doc_type='_doc', include_type_name=True)
bash: syntax error near unexpected token `index='my_index','
https://techoverflow.net/2019/05/02/how-to-fix-elasticsearch-types-cannot-be-provided-in-put-mapping-requests-unless-the-include_type_name-parameter-is-set-to-true/
```
sudo nano /home/sk1f/.local/lib/python2.7/site-packages/elasticsearch/client/indices.py
```
# Test

```
@timestamp:
    Mar 22, 2021 @ 21:04:34.573
tags:
    T1107_File_Deletion
service.type:
    auditd
host.id:
    747e9885cd784617b51147f4cef404c9
host.containerized:
    false
host.ip:
    10.0.2.15, fe80::285d:6448:f77e:488a
```
https://app.slack.com/client/T01S3CYDEQK/C01RNDGBEDV

Then from the menu add apps - incoming webhooks

# Webhook URL
```
https://hooks.slack.com/services/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

!add this webhook to rules.yaml in elastalert config.
```
Rule:
```
name: sk1f-slack-demo

type: frequency
num_events: 1

timeframe:
  minutes: 5


index: auditbeat-*

filter:
 - terms:
     service.type: "auditd"
 - terms:
     tags: "_File_Deletion"

alert:
- "slack"

slack:
-slack_webhook_url: "https://hooks.slack.com/servi$

```

elastalert-test-rule --config elastalert/example_rules/sk1f_auditd_rules_test.yaml
python3 /usr/bin/elastalert-test-rule /elastalert/example_rules/sk1f_auditd_rules_test.yaml
python -m pip install -U pip
elastalert-test-rule --config config.yaml example_rules/example_frequency.yaml

WARNING: The scripts elastalert, elastalert-create-index, elastalert-rule-from-kibana and elastalert-test-rule are installed in '/home/sk1f/.local/bin' which is not on PATH.
  Consider adding this directory to PATH or, if you prefer to suppress this warning, use --no-warn-script-location.
```
export PATH="$home/sk1f/.local/bin:$PATH"
```
sudo nano /elastalert/example_rules/sk1f_auditd_rules_test.yaml

```

python3 /usr/local/bin/elastalert-test-rule --config config.yaml /data/elk/elastalert-master/example_rules/example_frequency.yaml

```
# This seemed to work!
```
python3 /usr/local/bin/elastalert-test-rule --config config.yaml example_rules/example_frequency.yaml
```

# Exporting messages to SLACK (running as daemon)

```
python3 -m elastalert.elastalert --verbose --rule example_frequency.yaml
```












#Watcher - needs licence

```
https://www.elastic.co/guide/en/elasticsearch/reference/current/watcher-getting-started.html
```

