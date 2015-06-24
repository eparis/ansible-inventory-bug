# ansible-inventory-bug

Works:
ansible-playbook -i myinventory cluster.yml

```
TASK: [Print if in masters] *************************************************** 
skipping: [1.2.3.5]
skipping: [1.2.3.6]
ok: [1.2.3.4] => {
    "msg": "In masters!"
}

TASK: [Print if in nodes] ***************************************************** 
skipping: [1.2.3.4]
ok: [1.2.3.5] => {
    "msg": "In nodes!"
}
ok: [1.2.3.6] => {
    "msg": "In nodes!"
}

TASK: [Print if in both] ****************************************************** 
ok: [1.2.3.5] => {
    "msg": "In both!"
}
ok: [1.2.3.6] => {
    "msg": "In both!"
}
ok: [1.2.3.4] => {
    "msg": "In both!"
}
```

Fails:
ansible-playbook -i my.sh cluster.yml
```
TASK: [Print if in masters] *************************************************** 
fatal: [1.2.3.5] => Failed to template {% if inventory_hostname in [u'1.2.3.4'] %} True {% else %} False {% endif %}: template error while templating string: expected token ',', got 'string'
fatal: [1.2.3.6] => Failed to template {% if inventory_hostname in [u'1.2.3.4'] %} True {% else %} False {% endif %}: template error while templating string: expected token ',', got 'string'
fatal: [1.2.3.4] => Failed to template {% if inventory_hostname in [u'1.2.3.4'] %} True {% else %} False {% endif %}: template error while templating string: expected token ',', got 'string'

FATAL: all hosts have already failed -- aborting
```
