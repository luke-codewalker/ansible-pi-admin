# Ansible Pi Admin

The goal of this repository is to contain all the administration tasks of the Raspberry Pis floating around my network and the eventual automatization of these tasks with Ansible. 

The idea is to start with collecting all necessary tasks. Writing up some details about them, describe necessary (manual) steps and eventually code it with Ansible playbooks to make the tasks repeatable and declarative

> This is supposed to be a learning exercise for me in my non-critical home environment. Thus I will "reinvent the wheel" and hack a lot and *not* only use battle-tested solutions. But if you are interested in this journey and can also learn something from it, great!

## Tasks, Todos and Questions

This is the first step: listing all tasks I need to perform (list might grow over time). I will check them off once I have collected details about and described the task so that I can repeat it easily (not necessarily with Ansible). 

- [ ] prerequisites
    - [ ] giving fixed IP addresses. Only possible via Router?
        - [ ] add config for Ansible/document them somewhere
    - [ ] installing OS/flashing SD card
    - [ ] SSH setup (password vs key based), how far can this be automated?
    - [ ] ansible setup on control node and Python on managed node
    - [ ] sensible user management?
- [ ] k3s setup
    - [ ] Pi config (memory and something else?) for k3s
    - [ ] installing k3s (control plane or worker node)
    - [ ] ability to uninstall
    - [ ] repair, diagnose (logs, systemctl restart etc.?)
    - [ ] permissions/security? need to read up on this
- [ ] monitoring and logging setup (Grafana? Resource monitoring setup?)
- [ ] installing desired helm charts? Maybe maintain list of wanted helm charts somewhere?
- [ ] optional: remote management possibilities?
