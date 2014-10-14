# Logrotate role for Ansible

Ansible role for setting up automatic rotation and archival of log files.

## Requirements

Tested on Ubuntu 12.04 Server.

## Role Variables

The default variables are as follows:

    logrotate_compress:           'yes'                     # Whether to gzip rotated files.
    logrotate_conf_name:          'my_app_name'             # Name of the config file to be written in /etc/logrotate.d.
    logrotate_delay_compress:     'yes'                     # Whether to delay compression until the next rotation cycle (may solve file-in-use issues).
    logrotate_file_permissions:   0644                      # File permissions for rotated logs/archives.
    logrotate_log_dir:            '$HOME/log'               # Target directory containing log files.
    logrotate_log_extension:      'log'                     # File extension for log files.
    logrotate_ignore_empty:       'yes'                     # Whether to ignore empty log errors.
    logrotate_ignore_missing:     'yes'                     # Whether to ignore missing log errors.
    logrotate_rotate_frequency:   'monthly'                 # Frequency of rotation. Valid values are 'daily', 'monthly', 'yearly'.
    logrotate_rotate_count:       7                         # How many logs to rotate before the oldest one is deleted.
    logrotate_rotate_size:        '100M'                    # If logs reach this size, they will be rotated. Takes precedence over logrotate_rotate_frequency.
    logrotate_use_date_extension: 'yes'                     # Whether to append the date to rotated logs. If false, a number is used instead.
    logrotate_user:               '{{ ansible_ssh_user }}'  # Owner of rotated logs files.
    logrotate_user_group:         '{{ ansible_ssh_user }}'  # Group of rotated log files.

## Example Playbook

    - hosts: 'servers'
      roles:
        - role: 'ssilab.logrotate'
          logrotate_conf_name:        'my_app_name'
          logrotate_user:             '{{ deployment_user }}'
          logrotate_user_group:       '{{ deployment_user }}'
          logrotate_log_dir:          '{{ deployment_user_home}}/log'
          logrotate_log_extension:    'txt'
          logrotate_rotate_frequency: 'daily'
          logrotate_rotate_size:      '10M'
          logrotate_rotate_count:     7

# License

This playbook is provided 'as-is' under the conditions of the BSD license. No fitness for purpose is guaranteed or implied.