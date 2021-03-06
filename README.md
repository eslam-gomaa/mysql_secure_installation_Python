

# mysql_secure_installation_Python





## Features

A Python function that provides the functions of `mysql_secure_installation`

* Change MySQL Root Password - for a list of hosts i.e `localhost`, `127.0.0.1`, `::1`, .etc.
* Remove Anonymous User
* Disallow Root Login Remotely
* Remove Test Database



## WHY ?



* Python & **Idempotent** :sunglasses:
  * Means that when you run it again, will not re-execute the commands *If the desired state meets the current state*



---



## Usage



* Install the `MySQL-python` Library

```bash
# For Centos
yum insatll MySQL-python

# ------ ------ ------

# For ubuntu
apt-get install -y python-dev libmysqlclient-dev
pip install MySQL-python

# OR
apt install python3-mysqldb
```



---



#### use the function `mysql_secure_installation`



* For a Fresh MySQL Installation

```python
mysql_secure_installation(login_password='',
                          new_password='password22',
                          login_host='localhost',
                          hosts=['localhost',
                                 '::1',
                                 '127.0.0.1',
                                 'controller.linux.com',
                                 'controller'],
                          disallow_root_login_remotely=True,
                          remove_anonymous_user=True,
                          remove_test_db=True)
```



* Change Root password

```python
mysql_secure_installation(login_password='password22',
                          new_password='password55',
                          hosts=['localhost',
                                 '::1',
                                 '127.0.0.1',
                                 'controller.linux.com',
                                 'controller',
                                 'test'])
```



* Example Output

```bash
python mysql.py

{'remove_anonymous_user': 0, 'hosts_success': ['127.0.0.1', 'localhost', '::1'], 'disallow_root_remotely': None, 'hosts_failed': ['test', 'controller', 'controller.linux.com'], 'remove_test_db': 0, 'change_root_pwd': 1}
# 'disallow_root_remotely': None --> because it's "False" by default

python mysql.py

{'remove_anonymous_user': 0, 'stdout': 'Password of root@localhost Already meets the desired state', 'hosts_success': [], 'disallow_root_remotely': None, 'hosts_failed': [], 'remove_test_db': 0, 'change_root_pwd': 0}
```



---



## Input



| :Param                         | :Description                                                 | :Default      | :Type   |
| ------------------------------ | ------------------------------------------------------------ | ------------- | ------- |
| `login_password`               | Root's password to login to MySQL                            |               | String  |
| `new_password`                 | New desired Root password                                    |               | String  |
| `user`                         | MySQL user                                                   | root          | String  |
| `login_host`                   | host to connect to                                           | localhost     | String  |
| `hosts`                        | List of hosts for the provided user i.e `['localhost', '127.0.0.1', '::1']`, `Note:` all will have the same new password | [‘localhost’] | List    |
| `change_root_password`         |                                                              | True          | Boolean |
| `remove_anonymous_user`        |                                                              | True          | Boolean |
| `disallow_root_login_remotely` |                                                              | False         | Boolean |
| `remove_test_db`               |                                                              | True          | Boolean |



---



## Output

| Code | Meaning   | Description                                                  |
| ---- | --------- | ------------------------------------------------------------ |
| 0    | `Success` | When repeat –> `meet the desired state`                      |
| 1    | `Fail`    | **`change_root_pwd`** - will output `1` if failed to change the password of at least 1 host, for more info check `hosts_success` & `hosts_failed` |



---



Thank you 

[Eslam Gomaa](https://www.linkedin.com/in/eslam-gomaa/)

