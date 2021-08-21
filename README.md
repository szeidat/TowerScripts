Ansible Tower Scripts
=====================

A collection of Ansible Tower scripts

Requirements
------------

The following linux tools are required for the bash scripts. Versions noted were used for validation:

- **curl** (v7.61.1): For REST API calls
- **jq** (v1.5): For JSON data parsing 

Bash Scripts
------------

### tower-job-list

Usage:

```bash
$ tower-job-list --help

tower-job-list v0.2

    Retrieve the list of ansible tower jobs
    API Reference: https://docs.ansible.com/ansible-tower/3.8.2/html/towerapi/api_ref.html

Usage:

    tower-job-list [-t|--tower-host host] [-u|--username username] [-p|--password password] [-s|--status <choice>] [-h|--help]

Options:

    -t, --tower-host  tower server hostname or ip address
    -u, --username    tower username (default: prompt for username)
    -p, --password    tower password (default: prompt for password)
    -s, --status      filter jobs by status (choice: new, pending, waiting, running, successful, failed, error, canceled)
    -h, --help        display this message and exit
```

Example:

```bash
$ tower-job-list -t ansibletower.dev.internal -u admin

Password:******

Retrieving data. Please wait...

ID     Name                                                                 Job Type  Launch Type  Status      Started (UTC)        Elapsed
--     ----                                                                 --------  -----------  ------      -------------        -------
5573   Hosts fact collection                                                run       scheduled    failed      2021-02-20 08:30:05  47.122
5578   Servers Access-Validate awx_dev service account                      run       manual       failed      2021-02-20 14:47:20  18.039
5580   Servers Access-Validate awx_dev service account                      run       manual       failed      2021-02-20 14:51:04  17.965
5582   Servers Access-Validate awx_dev service account                      run       manual       failed      2021-02-20 14:52:41  17.688
5584   Servers Access-Validate awx_dev service account                      run       manual       failed      2021-02-20 14:55:53  17.405
5586   Servers Access-Validate awx_dev service account                      run       manual       failed      2021-02-20 15:03:10  153.341
5588   Servers Access-Validate awx_dev service account                      run       manual       failed      2021-02-20 15:07:29  291.486
5600   Hosts fact collection                                                run       scheduled    failed      2021-02-21 08:30:05  46.865
5619   Configuration management: Web Server Farm                            check     manual       failed      2021-02-22 05:03:03  45.617
5621   Hosts fact collection                                                run       scheduled    failed      2021-02-22 08:30:03  46.596
5634   Configuration management: Web Server Farm                            check     manual       successful  2021-02-23 01:20:51  22.118
5642   Hosts fact collection                                                run       scheduled    failed      2021-02-23 08:30:22  48.298
5654   Configuration management: Web Server Farm                            check     manual       successful  2021-02-24 00:30:31  29.831
5656   Servers Access-Validate awx_tst service account                      run       manual       failed      2021-02-24 01:18:33  70.061
5662   Servers Access-Validate awx_dev service account                      run       manual       failed      2021-02-24 01:22:05  380.723
5664   Configuration management: Web Server Farm                            check     manual       failed      2021-02-24 02:29:50  6.843
5667   Configuration management: Web Server Farm                            check     manual       successful  2021-02-24 02:31:00  25.787
5673   Hosts fact collection                                                run       scheduled    failed      2021-02-24 08:30:11  48.433
5688   Configuration management: Web Server Farm                            check     manual       failed      2021-02-25 01:49:49  279.019
5690   Configuration management: Web Server Farm                            run       manual       successful  2021-02-25 02:14:47  34.334
5692   Configuration management: Web Server Farm                            run       manual       successful  2021-02-25 02:25:24  34.678
5694   Configuration management: Web Server Farm                            run       manual       successful  2021-02-25 02:27:29  35.879
```

### tower-job-summary

Usage:

```bash
$ tower-job-summary v0.2

    Retrieve host summaries for an ansible tower job
    API Reference: https://docs.ansible.com/ansible-tower/3.8.2/html/towerapi/api_ref.html

Usage:

    tower-job-summary [-t|--tower-host host] [-u|--username username] [-p|--password password] [-h|--help] job-id

Options:

    -t, --tower-host  tower server hostname or ip address
    -u, --username    tower username (default: prompt for username)
    -p, --password    tower password (default: prompt for password)
    -h, --help        display this message and exit
    job-id            tower job id
```

Example:

```bash
$ tower-job-summary -t ansibletower.dev.internal -u admin 6215

Password:******

Retrieving data. Please wait.

Host                         Ok  Changed  Unreachable  Failed  Skipped  Rescued  Ignored
----                         --  -------  -----------  ------  -------  -------  -------
auserver001.dev.internal  25  4        0            0       15       0        0
auserver002.dev.internal  25  4        0            0       15       0        0
```

### tower-job-output

Usage:

```bash
$ tower-job-output --help

tower-job-output v0.3

    Retrieve standard output for an ansible tower job
    API Reference: https://docs.ansible.com/ansible-tower/3.8.2/html/towerapi/api_ref.html

Usage:

    tower-job-output [-t|--tower-host host] [-u|--username username] [-p|--password password] [-o|--output filename [-f|--format ansi|html]] [-l|--limit hostnames] [-c|--changed] [-h|--help] job-id

Options:

    -t, --tower-host  tower server hostname or ip address
    -u, --username    tower username (default: prompt for username)
    -p, --password    tower password (default: prompt for password)
    -o, --output      save output to filename
    -f, --format      file format (choice: ansi, html, txt. default: ansi)
    -l, --limit       show output from hostnames only (comma separated list. cannot be used with html output format)
    -c, --changed     show output from tasks with changed status only (cannot be used with html output format)
    -h, --help        display this message and exit
    job-id            tower job id
```

Example:

```bash
$ tower-job-output -t ansibletower.dev.internal -u admin -o output.html -f html 6215

Password:

Retrieving data. Please wait.
Output saved to output.html
```
