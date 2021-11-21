## Playbook basic run

```bash
[usman@linux 04-lamp-server]$ ansible-playbook  -c local -i 127.0.0.1, valut-basic.yml 

PLAY [127.0.0.1] ********************************************************************

TASK [Echo the API Key to use as ENV VAR] *******************************************
changed: [127.0.0.1]

TASK [Showing result] ***************************************************************
ok: [127.0.0.1] => {
    "echo_result.stdout": "dadkb2329u3ojasodijasod9"
}

PLAY RECAP **************************************************************************
127.0.0.1                  : ok=2    changed=1    unreachable=0    failed=0    skipped=0    rescued=0    ignored=0   
```

## Encrypting api-key.yml file in vars folder

```bash
[usman@linux 04-lamp-server]$ ansible-vault encrypt vars/api_key.yml 
New Vault password: YOUR_PASS
Confirm New Vault password: YOUR_PASS
Encryption successful
```

## NOW our file var/api-key.yml is encrypted with AES256 encryption code

```bash
[usman@linux 04-lamp-server]$ ansible-playbook  -c local -i 127.0.0.1, valut-basic.yml
ERROR! Attempting to decrypt but no vault secrets found
```

## TO RUN PLAYBOOK,  WE NEED TO PROVIDE THE VALUT PASS BY PASSING ARGUMENT "--ask-valut-pass"

```bash
[usman@linux 04-lamp-server]$ ansible-playbook  -c local -i 127.0.0.1, valut-basic.yml --ask-vault-pass
Vault password: 

PLAY [127.0.0.1] ********************************************************************

TASK [Echo the API Key to use as ENV VAR] *******************************************
changed: [127.0.0.1]

TASK [Showing result] ***************************************************************
ok: [127.0.0.1] => {
    "echo_result.stdout": "dadkb2329u3ojasodijasod9"
}

PLAY RECAP **************************************************************************
127.0.0.1                  : ok=2    changed=1    unreachable=0    failed=0    skipped=0    rescued=0    ignored=0   

```

## TO EDIT A ENCRYPTED VALUT FILE ON RUN-TIME



```bash
[usman@linux 04-lamp-server]$ ansible-vault edit vars/api_key.yml
Vault password: YOUR_PASS
```

## TO GIVE A NEW PASS THEN USE "rekey"

```bash
[usman@linux 04-lamp-server]$ ansible-vault rekey vars/api_key.yml
Vault password: YOUR_PASS
New Vault password: YOUR_NEW_PASS
Confirm New Vault password: YOUR_NEW_PASS
Rekey successful
```



## TO DECRYPT VALUT PASS USE THE DECRYPT FUNCTIION

```bash
[usman@linux 04-lamp-server]$ ansible-vault decrypt vars/api_key.yml
Vault password: YOUR_PASS
Decryption successful
[usman@linux 04-lamp-server]$ ansible-playbook  -c local -i 127.0.0.1, valut-basic.yml 

PLAY [127.0.0.1] ********************************************************************

TASK [Echo the API Key to use as ENV VAR] *******************************************
changed: [127.0.0.1]

TASK [Showing result] ***************************************************************
ok: [127.0.0.1] => {
    "echo_result.stdout": "dadkb2329u3ojasodijasod9"
}

PLAY RECAP **************************************************************************
127.0.0.1                  : ok=2    changed=1    unreachable=0    failed=0    skipped=0    rescued=0    ignored=0  
```


