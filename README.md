# Ansible Requirements Updater

**Update your requirements.yml with this unsightly Ansible playbook.**

This is one of the gookiest Ansible playbooks I've ever written.

But it does something I need, and it's a lot faster than doing it manually, and I do it every few months. So it was worth spending two hours automating the process on a Friday night while watching a Blues game.

The playbook does the following:

  1. Reads in a list of role requirements from an existing `requirements.yml` file (at `requirements_file_path`).
  2. Loops through all the roles in that list, and gets the latest role version string from Ansible Galaxy.
  3. Generates a new requirements list.
  4. Writes the new list to the `requirements.yml` file.

If you're really daring and had a few drinks, you can set `requirements_file_backup` to `false`, and overwrite your artisinally-handcrafted requirements file with whatever this playbook disgorges 🤮.

You might be wondering at this point, why don't you just run `ansible-galaxy update -r requirements.yml`? Well, unfortunately, `update` is not a thing, and never will be, for roles on Ansible Galaxy. Collections _might_ someday get that functionality (so we can stop updating our `requirements.yml` files by hand like neanderthals), but until then, you can do it manually, or trust your life to this playbook. I know what _I'd_ do.

## Caveats

  - This has only been tested with `geerlingguy.*` roles, and a few others which follow semantic versioning standards. Since Galaxy allows practically anything as a version (heck, you could probably throw a 🦑 in there and it would work), the playbook will likely break your requirements in new and interesting ways if you use roles that do strange things with versioning.
  - This playbook only handles requirements files with `roles` in them, not with `roles` and `collections`. If you have any `collections` listed in your requirements file, this playbook will act like they don't exist and they will go 💥.
  - You should never write a playbook like this. It is dumb. It is inefficient. It is against every one of the best practices I espouse in my book [Ansible for DevOps](https://www.ansiblefordevops.com) and my blog posts on Ansible. But I did, so 🤷‍♂️.

## Usage

Run the playbook like so:

    ansible-playbook main.yml -e "requirements_file_path=path/to/a/requirements.yml"

Go get a coffee (☕️) – it's going to take a while because of how horrifically inefficient it is to use Ansible as a programming language like this playbook does.

Cross your fingers (🤞) and hope it works.

> **Note**: It is _highly_ recommended you track your `requirements.yml` file in a git repository. That way if this playbook mangles it horrifically, you can `git restore requirements.yml` and act like nothing happened 🤐.

## License

MIT.

## Author Information

This playbook was brought into its miserable existence by [Jeff Geerling](https://www.jeffgeerling.com/), author of [Ansible for DevOps](https://www.ansiblefordevops.com/) and [Ansible for Kubernetes](https://www.ansibleforkubernetes.com).