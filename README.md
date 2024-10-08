This project is aimed at completely transforming my HomeLab to IaC.
For now, the deployment should work from start to finish, but my goal is to increase the quality and robustness and make the playbook somewhat usable by other people.

Install dependencies with:
```cmd
ansible-galaxy install -r requirements.yml
```
Create an inventory.yml and start the playbook with
```cmd
ansible-playbook server.yml -i inventory.yml --vault-password-file ~/vault-pass
```
