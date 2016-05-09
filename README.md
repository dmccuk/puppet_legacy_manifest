Welcome to the puppet manifest creator
======================================

* I'm developing this script with the main focus of trying to manage legacy servers that weren't built by puppet.

It's useful for the following
-----------------------------

 1. Quickly creating a manifest of your exisiting servers
 2. Locally apply the manifest back via cron from the apply.pp fine created (user setup required).
 3. Move the manifest (under the server name) into a puppet master. Set the role to the servername.
 4. Create/rebuild legacy servers based on this manifest

Usage
-----

I assume you have git installed already.

 1. Clone the Repo - git clone https://github.com/dmccuk/puppet_legacy_manifest.git
 2. cd into the cloned directory. Examples in each of the files described below:
      * Update "files.dm" with the name and location of what you want to manage.
      * Update "services_packages.dm" with the serivce name and the package name.
 3. To run:
      * ./manifest_creator.sh 
 4. The script will run and create the following directory tree:
      * /opt/HOSTNAME
      * The manifests will be created under this DIR.
      * an "apply.pp" script will be created that you can run to apply the maifest back to the server.

Please feel free to clone or update 
