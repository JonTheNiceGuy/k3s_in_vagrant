# K3S in Vagrant with Ansible

I've dabbled quite a bit at getting various projects to build in [Vagrant](https://vagrantup.com).
On this occasion, I'm using [Ansible](https://ansible.com) to provision [K3S](https://k3s.io/).

## Dependencies

You need to have installed Vagrant and [Virtualbox](https://virtualbox.org). If you later want to
run Kubernetes actions from outside the cluster, you should install [`direnv`](https://direnv.net),
add the [direnv hooks](https://direnv.net/docs/hook.html) and then run `direnv allow`. You will
then also, of course, need [`kubectl`](https://kubernetes.io/docs/tasks/tools/#kubectl).

## Running this script

Run `vagrant up`

## Issues/Comments/Concerns?

I welcome any proposed updates or comments, but please be aware, this has scratched a particular
itch for me, and your proposals may not be accepted. I fully reserve the right to archive this
repository at any point for later use.

## Security concerns

If you've got a particular concern about some security-related aspect of the content in this repo,
please address it directly to [me](mailto:jon@sprig.gs). Thanks.
