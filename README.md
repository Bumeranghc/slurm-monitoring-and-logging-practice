# Slurm Monitoring ang Logging practice
Generate ssh key pair in 'files' directory and name it 'monlog'

Run Vagrant with:

```
vagrant up
```

Connect to control node with:

```
vagrant ssh controlnode
```

Copy ansible directory and align file permissions

Run playbook with:

```
ansible-playbook playbook.yml
```