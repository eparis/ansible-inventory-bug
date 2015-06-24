# ansible-inventory-bug

Works:
ansible-playbook -i myinventory cluster.yml

Fails:
ansible-playbook -i my.sh cluster.yml

TASK: [Print if in masters] *************************************************** 
fatal: [1.2.3.5] => Failed to template {% if inventory_hostname in [u'1.2.3.4'] %} True {% else %} False {% endif %}: template error while templating string: expected token ',', got 'string'
