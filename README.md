puppet manifest creator
=======================
This is a generic script that creates a complete puppet manifest based on input from the user. Add files, services, packages (adding more soon) to the config files and this script will generate all the required puppet code to either apply locally back to your node or move to a puppet master using the role created when the script runs. It enables quick management of your legacy servers but also provides a way to manage the code once it's been generated.

Use case
--------
 1. Quickly creating a manifest of your exisiting servers.
 2. Locally apply the manifest back from the apply.pp script generated by the script.
 3. Move the manifest (under the server name) into a puppet master. Set the role and manage with your master.
 4. Create/rebuild legacy servers based on the manifest you create.

Changelog
---------
 * [ Added hostname factorisation. All .erb files are checked for the hostname of the server and replaced by @hostname ]
 * [ Created a role that can be run on a puppet master based on the files managed by the script ]
 * [ Added the ability to create a "file_line" managed config file in addition to a template ]
 * [ catered for hostnames with - and changed them to _ ]
 * [ Added fstab (mount) as a defualt option. It doesn't need to be added to any configs ]

Dependencies
------------
 * To use file_line, download puppetlabs-stdlib to the /opt/HOST_ directory.
 * Puppet version 3.0 or above
 * Git

Usage
-----
 1. Clone the Repo - git clone https://github.com/dmccuk/puppet_legacy_manifest.git
 2. cd into the cloned directory. Examples in each of the files described below:
      * Update "files_managed_by_templates.dm" with the name and location of what you want to manage.
      * Update "services_packages.dm" with the serivce name and the package name.
      * update "files_managed_by_file_line.dm" with the files you wish to create a "file_line" output for.
 3. To run:
      * ./manifest_creator.sh 
 4. The script will run and create the following directory tree:
      * /opt/$hostname
      * The manifests will be created under this DIR.
      * an "apply.pp" script will be created that you can run to apply the maifest back to the server. See apply.pp for more information once run.
      * A role_$hostname will alos be created so you can move the code to a puppet master and manage via the role.

Development
===========
Plans are to add the following:

  * Data abstraction of IP addresses where appropiate.
  * Cater for user defined "users" to be captured by the script and added into the manifest.
  * Add metadata.json file to all manifests.

Issues:
------
[1]
If you see this when running puppet apply:

    Error: Evaluation Error: Error while evaluating a Resource Statement, Invalid resource type file_line at /opt/server_name/sshd_config/manifests/init.pp:3:3 on node server1

You need to download and install puppetlabs-stdlib to your working directory. In this case it's /opt/$HOST_. The file_line type requires stdlib is installed.

    # puppet module install -i . -f  puppetlabs-stdlib
    Notice: Preparing to install into /opt/fedora_22 ...
    Notice: Downloading from https://forgeapi.puppetlabs.com ...
    Notice: Installing -- do not interrupt ...

Now run puppet apply again.
