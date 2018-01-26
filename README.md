mattermost-github
=================

A role that installs and can configure [mattermost-github-integration](https://github.com/softdevteam/mattermost-github-integration).

Requirements
------------

An ansible 2.0+ installation.

Role Variables
--------------

Available variables are listed below, along with default values (please see `defaults/main.yml`):

    mattermost_github_install_root: '/opt/mattermost-github'

The location where the repository will be checked-out.

    mattermost_github_user: mattermost-github

System user to run the service as, will be created if it does not exist

    mattermost_github_config_username: "GitHub"

The username that is shown in Mattermost.
The "Enable integrations to override usernames" setting (or ServiceSettings.EnablePostUsernameOverride in config.json) must be set to 'true'.

    mattermost_github_config_icon_url: ""

The URL to the icon to use for the user in Mattermost.
The "Enable integrations to override profile picture icons" (or ServiceSettings.EnablePostIconOverridesetting in config.json) must be 'true'.

    mattermost_github_config_secret: "CHANGEME"

The secret to authenticate the sent hooks from GitHub.

    mattermost_github_config_show_avatars: True

Whether or not to show the GitHub user's avatar in the messages.

    mattermost_github_config_server_hook: '/'

The path where mattermost-github-integration will accept HTTP requests.

    mattermost_github_config_server_address: '127.0.0.1'

The listen-address for mattermost-github-integration

    mattermost_github_config_server_port: 8080

The port on which mattermost-github-integration should listen.

    mattermost_github_config_mattermost_webhook_urls: ''

All webhook config as a string, copied verbatim into MATTERMOST_WEBHOOK_URLS.

    mattermost_github_config_ignore_actions: ''

All ignored events, is copied verbatim into GITHUB_IGNORE_ACTIONS.

    mattermost_github_version: 'master'

The version (or git revision) to check out when installing.

Example Playbook
----------------

```yaml
- hosts: servers
  roles:
     - role: pieterlexis.mattermost-github
       mattermost_github_config_server_hook: '/hooks/github',
       mattermost_github_config_secret: 'eCWwdkxxue8F0Lkpcd7U9EASYyBLatOl'
       mattermost_github_config_mattermost_webhook_urls: |
         default: None,
         'MyOrg/some-repo': ('https://mattermost.example.com/hooks/1234567890abcd', 'github'),
         'MyOrg/second-repo': ('https://mattermost.example.net/hooks/abcd1234567890', 'special-channel')
       mattermost_github_config_ignore_actions: |
         "issues": ["label", "assign"]
```

License
-------

MIT

Author Information
------------------

 * Pieter Lexis
