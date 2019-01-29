### Pré requis
```
https://docs.microsoft.com/en-us/azure/virtual-machines/linux/ansible-install-configure?toc=%2Fen-us%2Fazure%2Fansible%2Ftoc.json&bc=%2Fen-us%2Fazure%2Fbread%2Ftoc.json#file-credentials
```

### Playbook
```
---
- name: azure playbook
  hosts: localhost
  roles:
    - azure
  tasks:
    - include_tasks: roles/azure/tasks/create.yml
      when: create is defined

    - include_tasks: roles/azure/tasks/delete.yml
      when: delete is defined

    - include_tasks: roles/azure/tasks/get_info.yml
      when: info is defined
```


### Utilisation
Les variables sont dans default/main.yml  
Pour surcharger une variable durant l'execution utiliser l'option -e: -e nom_variable=valeur_variable  
exemple:  
```
ansible-playbook -i inventory -t delete -e moninstance_id=i-05bc81adff0bbb43b ec2.yml
```

#### Creer une instance
```
[ansible@fcd1f181a740 ~]$ ansible-playbook -i inventory azure.yml -e create=true
[...]
PLAY RECAP *********************************************************************************************************************************************************************
localhost                  : ok=10   changed=6    unreachable=0    failed=0  
```

#### Get public ip
```
[ansible@fcd1f181a740 ~]$ ansible-playbook -i inventory azure.yml -e info=true
[...]
PLAY RECAP *********************************************************************************************************************************************************************
localhost                  : ok=4    changed=0    unreachable=0    failed=0   
````


#### Delete instance
```
[ansible@fcd1f181a740 ~]$ ansible-playbook -i inventory azure.yml -e delete=true
PLAY RECAP *********************************************************************************************************************************************************************
localhost                  : ok=12   changed=6    unreachable=0    failed=0  
```
