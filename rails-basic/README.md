## What is rails-basic?

It is a set of [ansible](http://www.ansible.com/home) roles to provision 1 or more servers to run a pretty typical rails application.

## Dependencies

Ansible version 1.6+ must be installed to use this playbook.

`$ ansible-galaxy install nickjj.user nickjj.security nickjj.postgres nickjj.ruby nickjj.nodejs nickjj.nginx nickjj.rails DavidWittman.redis`

If you get permission errors then run the command with `sudo`. If you get an errors saying you already have them then add `--force` to the end of the command.

## Roles used

If you are having issues running any tasks then please consult with the documentation for that specific role.

- `nickjj.user` https://github.com/nickjj/ansible-user
- `nickjj.security` https://github.com/nickjj/ansible-security
- `nickjj.postgres` https://github.com/nickjj/ansible-postgres
- `nickjj.ruby` https://github.com/nickjj/ansible-ruby
- `nickjj.nodejs` https://github.com/nickjj/ansible-nodejs
- `nickjj.nginx` https://github.com/nickjj/ansible-nginx
- `DavidWittman.redis` https://github.com/DavidWittman/ansible-redis

## Things you need to provide

You need to have a rails application hosted on github, bitbucket or some other remote git host. It can be a default rails application however the app server you choose must write out a unix socket. You can see what you need to change in `group_vars/all.yml`.

## Running the playbook

After you have configured `group_vars/all.yml` then it is go time. You can run the playbook by making sure you are in the `rails-basic` folder and then entering this command into your terminal:

`$ ansible-playbook site.yml -i inventory/ -kK`

You only need to supply the `-kK` flags on the first run. These are short for telling ansible to prompt you for the user's password and the sudo password. Once you do this ansible will kick in and provision the server to use ssh keys as long as everything is setup properly.

## Video tutorial

Not available right now.

## Having issues and are wondering what to do?

Make sure you check out the [general documentation](https://github.com/nickjj/ansible-playbooks#general-information-and-terminology). Please open a ticket if you find a bug.

## Important things left to do for this playbook

A way to manage your rails processes. This is more complicated than it appears at first glance because each rails app is very different. You may have sidekiq while I do not. Perhaps you're using unicorn while I'm using puma. There's many combinations.

One thing is for sure, the process actions will be coded with SystemV (`/etc/init.d`) and then monitored with monit. I just have not yet had the time to think of a way to set it all up where people can control and monitor arbitrary processes in an easy way. If anyone wants to discuss this then feel free to open a ticket.

## License

MIT